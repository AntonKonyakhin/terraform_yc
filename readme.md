### Задача 2. Создание aws ec2 или yandex_compute_instance через терраформ.  


1) В каталоге terraform вашего основного репозитория, который был создан в начале курсе, создайте файл main.tf и versions.tf.  

счоздал main.tf и versions.tf
```
root@anton-v-m:~/yandex-cloud-terraform# ll
total 20
drwxr-xr-x  3 root root 4096 июн  4 22:42 ./
drwx------ 30 root root 4096 июн  4 22:40 ../
drwxr-xr-x  8 root root 4096 июн  4 01:31 .git/
-rw-r--r--  1 root root 1560 июн  4 01:08 main.tf
-rw-r--r--  1 root root  131 июн  4 00:15 versions.tf


```

2. Зарегистрируйте провайдер:

- для yandex.cloud. Подробную инструкцию можно найти здесь.  

прописал настройки, выполнил terraform init
```
root@anton-v-m:~/yandex-cloud-terraform# cat ~/.terraformrc
provider_installation {
  network_mirror {
    url = "https://terraform-mirror.yandexcloud.net/"
    include = ["registry.terraform.io/*/*"]
}
  direct {
    exclude = ["registry.terraform.io/*/*"]
}
}

```

```
root@anton-v-m:~/yandex-cloud-terraform# cat versions.tf 
terraform {
  required_providers {
    yandex = {
      source = "yandex-cloud/yandex"
    }
  }
  required_version = ">= 0.13"
}

```

```
root@anton-v-m:~/yandex-cloud-terraform# terraform init

Initializing the backend...

Initializing provider plugins...
- Finding latest version of yandex-cloud/yandex...
- Installing yandex-cloud/yandex v0.75.0...
- Installed yandex-cloud/yandex v0.75.0 (unauthenticated)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

3) Внимание! В гит репозиторий нельзя пушить ваши личные ключи доступа к аккаунту.Поэтому в предыдущем задании мы указывали их в виде переменных окружения.  
выполнил export 

```
export YC_TOKEN="***"
export YC_CLOUD_ID="***"
```

4. В файле main.tf воспользуйтесь блоком data "aws_ami для поиска ami образа последнего Ubuntu. 

не знаю, что имелось ввиду, в YC поискал образы с помощью команды:
```
yc compute image list --folder-id standard-images
```

5) В файле main.tf создайте рессурс
- yandex_compute_image.  
создал 2 виртуальные машины по мануалу от Яндекс
https://cloud.yandex.ru/docs/tutorials/infrastructure-management/terraform-quickstart


6. Если вы выполнили первый пункт, то добейтесь того, что бы команда terraform plan выполнялась без ошибок.

выполнился без ошибок
```
root@anton-v-m:~/yandex-cloud-terraform# terraform plan
```



В качестве результата задания предоставьте:  

Ответ на вопрос: 
1. при помощи какого инструмента (из разобранных на прошлом занятии) можно создать свой образ ami?  

2. Ссылку на репозиторий с исходной конфигурацией терраформа.  
https://github.com/AntonKonyakhin/terraform_yc

