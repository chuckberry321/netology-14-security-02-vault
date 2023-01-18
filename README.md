# Домашнее задание к занятию "14.2 Синхронизация секретов с внешними сервисами. Vault"

## Задача 1: Работа с модулем Vault

### Ответ:

Выводы всех команд приведены ниже (убрал часть вывода у Fedora, ну слишком длинный получился... ):

``` vagrant@ubuntu2010:~/netology-14-2$ kubectl apply -f vault-pod.yml
pod/14.2-netology-vault created 
vagrant@ubuntu2010:~/netology-14-2$ kubectl get pod 14.2-netology-vault -o json | jq -c '.status.podIPs'
[{"ip":"172.17.0.3"}] 
vagrant@ubuntu2010:~/netology-14-2$ kubectl run -i --tty fedora --image=fedora --restart=Never -- sh 
If you don't see a command prompt, try pressing enter. 
sh-5.2# dnf -y install pip
Fedora 37 - x86_64                                                                                                                                                                                           3.7 MB/s |  64 MB     00:17
-------------------------
Installed:
  python3-pip-22.2.2-3.fc37.noarch                                                                                  python3-setuptools-62.6.0-2.fc37.noarch

Complete!
sh-5.2# pip install hvac
Collecting hvac
----------------------------------------  
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
sh-5.2# python3 test.py
{'request_id': '41d7b9f3-50c9-bc16-b341-fdf464927434', 'lease_id': '', 'renewable': False, 'lease_duration': 0, 'data': {'data': {'netology': 'Big secret!!!'}, 'metadata': {'created_time': '2023-01-18T15:01:47.41350051Z', 'custom_metadata': None, 'deletion_time': '', 'destroyed': False, 'version': 3}}, 'wrap_info': None, 'warnings': None, 'auth': None}
sh-5.2#
vagrant@ubuntu2010:~/netology-14-2$ kubectl get po
NAME                  READY   STATUS    RESTARTS      AGE
14.2-netology-vault   1/1     Running   0             22m
fedora                1/1     Running   1 (46s ago)   5m22s
vagrant@ubuntu2010:~/netology-14-2$
```
