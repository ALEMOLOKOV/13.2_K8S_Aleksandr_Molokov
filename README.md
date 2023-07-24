# 13.2_K8S_Aleksandr_Molokov

### Задание 1

**Что нужно сделать**

Создать Deployment приложения, использующего локальный PV, созданный вручную.

1. Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
2. Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
3. Продемонстрировать, что multitool может читать файл, в который busybox пишет каждые пять секунд в общей директории. 
4. Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему.
5. Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV.  Продемонстрировать что произошло с файлом после удаления PV. Пояснить, почему.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

### Ответ

#### ![Deployment](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/blob/ce631bb93492079031b043678b4eada100d4bfee/deployment_pv.yaml)

#### ![PV](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/blob/ce631bb93492079031b043678b4eada100d4bfee/pv.yaml)

#### ![PVC](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/blob/ce631bb93492079031b043678b4eada100d4bfee/pvc.yaml)

#### Multitool может видеть и читать файлы, которые пишет Busybox

![multitool видит что пишет busybox](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/a03fcef7-08a0-46af-be6e-3df8161acf00)

#### Удаление Deployment и PVC

![pv после удаления dep pvc](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/58429afe-b95c-4d32-a59a-70cc211ba433)

#### Статус PV изменился с Bound на Released, т.к. к нему не привязана PVC

#### Состояние PV после удаления

![состояние после удаления pv](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/6708528a-84a0-4665-8f94-c65fcca442af)

#### Созданный файл Hello.txt сохранися на ноде в папке, указанной в конфиг файле PV. После удаления PV файл так и остался в папке т.к. это локальные хранилище.

### ------

### Задание 2

**Что нужно сделать**

Создать Deployment приложения, которое может хранить файлы на NFS с динамическим созданием PV.

1. Включить и настроить NFS-сервер на MicroK8S.
2. Создать Deployment приложения состоящего из multitool, и подключить к нему PV, созданный автоматически на сервере NFS.
3. Продемонстрировать возможность чтения и записи файла изнутри пода. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

### Ответ

#### Включение и настройка NFS-сервера на MicroK8S + установка nfs-common

![enable community](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/75f1bd98-c1ea-44b9-b589-beca0bfa1d68)

![enable nfs](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/8cfbc330-7bb3-4202-b168-0915d94a5e7f)

![install nfs-common](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/f3487947-97a3-4cd2-a7f4-b95c5aed3ae7)

#### ![Deployment](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/blob/fce103771926eb45abe37534f4c16986c6762d03/deployment.yaml)

#### ![PVC-NFS](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/blob/5b06e125f5be029945005ed99f48e71f8405c736/pvc-nfs.yaml)

#### Статусы Deployment/sc/pv/pvc/Pods

![deploy-pvc-pv-sc](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/61756228-6d47-498d-86ce-e4569b84e7b4)

#### Доступ чтение и запись с пода

![чтение и запись проверка к ноды](https://github.com/ALEMOLOKOV/13.2_K8S_Aleksandr_Molokov/assets/109212419/8b3fc0e8-3cf4-469e-a039-ee9d583e1adf)






