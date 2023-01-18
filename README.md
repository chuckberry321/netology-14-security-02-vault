# Домашнее задание к занятию "14.2 Синхронизация секретов с внешними сервисами. Vault"

## Задача 1: Работа с модулем Vault

### Ответ:

Выводы всех команд приведены ниже:

``` vagrant@ubuntu2010:~/netology-14-2$ kubectl apply -f vault-pod.yml
pod/14.2-netology-vault created 
vagrant@ubuntu2010:~/netology-14-2$ kubectl get pod 14.2-netology-vault -o json | jq -c '.status.podIPs'
[{"ip":"172.17.0.3"}] 
vagrant@ubuntu2010:~/netology-14-2$ kubectl run -i --tty fedora --image=fedora --restart=Never -- sh 
If you don't see a command prompt, try pressing enter. 
sh-5.2# dnf -y install pip
Fedora 37 - x86_64                                                                                                                                                                                           3.7 MB/s |  64 MB     00:17
Fedora 37 openh264 (From Cisco) - x86_64                                                                                                                                                                     1.1 kB/s | 2.5 kB     00:02
Fedora Modular 37 - x86_64                                                                                                                                                                                   1.8 MB/s | 3.0 MB     00:01
Fedora 37 - x86_64 - Updates                                                                                                                                                                                 1.4 MB/s |  21 MB     00:15
Fedora Modular 37 - x86_64 - Updates                                                                                                                                                                         752 kB/s | 1.1 MB     00:01
Last metadata expiration check: 0:00:01 ago on Wed Jan 18 14:58:58 2023.
Dependencies resolved.
=============================================================================================================================================================================================================================================
 Package                                                         Architecture                                        Version                                                      Repository                                            Size
=============================================================================================================================================================================================================================================
Installing:
 python3-pip                                                     noarch                                              22.2.2-3.fc37                                                updates                                              3.1 M
Installing weak dependencies:
 python3-setuptools                                              noarch                                              62.6.0-2.fc37                                                fedora                                               1.6 M

Transaction Summary
=============================================================================================================================================================================================================================================
Install  2 Packages

Total download size: 4.7 M
Installed size: 23 M
Downloading Packages:
(1/2): python3-setuptools-62.6.0-2.fc37.noarch.rpm                                                                                                                                                           1.9 MB/s | 1.6 MB     00:00
(2/2): python3-pip-22.2.2-3.fc37.noarch.rpm                                                                                                                                                                  1.9 MB/s | 3.1 MB     00:01
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                                                        1.6 MB/s | 4.7 MB     00:03
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                                                                     1/1
  Installing       : python3-setuptools-62.6.0-2.fc37.noarch                                                                                                                                                                             1/2
  Installing       : python3-pip-22.2.2-3.fc37.noarch                                                                                                                                                                                    2/2
  Running scriptlet: python3-pip-22.2.2-3.fc37.noarch                                                                                                                                                                                    2/2
  Verifying        : python3-setuptools-62.6.0-2.fc37.noarch                                                                                                                                                                             1/2
  Verifying        : python3-pip-22.2.2-3.fc37.noarch                                                                                                                                                                                    2/2

Installed:
  python3-pip-22.2.2-3.fc37.noarch                                                                                  python3-setuptools-62.6.0-2.fc37.noarch

Complete!
sh-5.2# pip install hvac
Collecting hvac
  Using cached hvac-1.0.2-py3-none-any.whl (143 kB)
Collecting pyhcl<0.5.0,>=0.4.4
  Using cached pyhcl-0.4.4.tar.gz (61 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting requests<3.0.0,>=2.27.1
  Downloading requests-2.28.2-py3-none-any.whl (62 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 62.8/62.8 kB 692.3 kB/s eta 0:00:00
Collecting charset-normalizer<4,>=2
  Downloading charset_normalizer-3.0.1-cp311-cp311-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (196 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 196.8/196.8 kB 2.1 MB/s eta 0:00:00
Collecting idna<4,>=2.5
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.5/61.5 kB 2.9 MB/s eta 0:00:00
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.14-py2.py3-none-any.whl (140 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 140.6/140.6 kB 10.2 MB/s eta 0:00:00
Collecting certifi>=2017.4.17
  Downloading certifi-2022.12.7-py3-none-any.whl (155 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 155.3/155.3 kB 9.9 MB/s eta 0:00:00
Building wheels for collected packages: pyhcl
  Building wheel for pyhcl (pyproject.toml) ... done
  Created wheel for pyhcl: filename=pyhcl-0.4.4-py3-none-any.whl size=50127 sha256=c9b5f183ca21ea417f572e5623b70fd20ac82e3527ece1a4d93faa0da0ac3738
  Stored in directory: /root/.cache/pip/wheels/e4/f4/3a/691e55b36281820a2e2676ffd693a7f7a068fab60d89353d74
Successfully built pyhcl
Installing collected packages: pyhcl, charset-normalizer, urllib3, idna, certifi, requests, hvac
Successfully installed certifi-2022.12.7 charset-normalizer-3.0.1 hvac-1.0.2 idna-3.4 pyhcl-0.4.4 requests-2.28.2 urllib3-1.26.14
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
