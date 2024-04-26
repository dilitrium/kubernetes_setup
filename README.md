# Install k8s cluster with Kubespray on Yandex Cloud
# kubernetes_setup 

# Написан по мотивам доклада Ильи Крылова "Установка кластера Kubernetes"
# https://git.cloud-team.ru/lections/kubernetes_setup/raw/master/presentation.pdf
# https://www.youtube.com/watch?v=WFXlr0bVTAQ

Вся подготовка по установке сервера управления srv, установки нужных пакетов и зависимостей, скачивание из репозиториев kubespay
и подготовка для установки кластера выполняется автоматически на предыдущем шаге кодом из репозитория: 
https://github.com/vajierik/infr

Для полуавтоматического варианта установки, необходимо после установки сервара управления SRV:
```
  - зайти по ssh на эту ноду:  ssh ubuntu@<IP_adress>
  - запустить скрипт развёртывания кластера k8s: /opt/kubernetes_setup/cluster_install.sh
```
В этом варианте только два ручных действия:
  - Развёртывание srv из заранее скачанного репозитория https://github.com/vajierik/infr: terraform apply
  - Развёртывание кластера k8s с srv ноды: /opt/kubernetes_setup/cluster_install.sh

Для автоматического развёртывания понадобится:
```
  - раскомментировать в файле /scripts/k8s-provisioning.sh самую нижнюю строку: #/opt/kubernetes_setup/cluster_install.sh репозитория https://github.com/vajierik/infr
  - Запуск автоматического каскадного развёртывания из заранее скачанного репозитория https://github.com/vajierik/infr srv ноды и кластера k8s с неё: terraform apply
```

В примере использован первый вариант - полуавтоматический.
Но тестировался и полностью автоматический. 
Полуавтоматический вариант выбран для более полного контроля и дебагинга развёртывания кластера с учетом будущих возможных изменений в версиях.

## Create cloud resources and install k8s cluster
```
$ /opt/kubernetes_setup/cluster_install.sh
```

## Delete cloud resources
```
$ /opt/kubernetes_setup/cluster_destroy.sh
```

Результаты разворачивания инфрастурктуры и кластера:

![create cluster k8s](https://github.com/vajierik/kubernetes_setup/assets/150177457/6db1715a-49b4-413e-b9d4-5faec0bd90ce)




Полезные ссылки:

## Register in Yandex Cloud

https://cloud.yandex.ru

## Install Terraform client 

https://learn.hashicorp.com/terraform/getting-started/install
 https://cloud.yandex.ru/docs/tutorials/infrastructure-management/terraform-quickstart

## Install Ansible

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

## Install Kubectl

https://kubernetes.io/docs/tasks/tools/install-kubectl/

## Install Helm

https://helm.sh/docs/intro/install/

## Install jq (small CLI utility for JSON parsing)

https://stedolan.github.io/jq/

## Clone Kubespray repo and install Kubespray requirements
```
$ git clone https://github.com/vajierik/kubernetes_setup
cd /kubernetes_setup
$ git clone https://github.com/vajierik/kubespray
```
