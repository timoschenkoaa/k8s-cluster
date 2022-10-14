# Деплой кластера Kubernetes с помощью Ansible:

## Запускаем поочередно ansible playbook

- ansible-playbook -i inventory 01-deploy-vms.yaml --ask-vault-pass
- ansible-playbook -i inventory 02-configure-vms.yaml
- ansible-playbook -i inventory 03-generate-artifacts.yaml
- ansible-playbook -i inventory 04-deploy-etcd.yaml
- ansible-playbook -i inventory 05-initialize-master.yaml
- !!! В выводе работы плэйбука 05-initialize-master.yaml находим результат создания кластера, копируем токен и sha. Затем заменяем значения токена и sha в 06-add-nodes.yaml
- ansible-playbook -i inventory 06-add-nodes.yaml

## Теперь кластер готов к работе. На данном этапе средой запуска контейнеров служит Docker. Для перевода на ContainerD неоходимо запустить последний плэйбук
- ansible-playbook -i inventory 08-migrate-to-containerd.yml
