## Решение «Создание собственных модулей»

1. Создал my_own_module.py
2. Наполнил.
3. Использовал документацию Ansible (и stackoverflow).
4. Проверил модуль локально (для проверки используем значения из файла для тестирования test_my_own_module.json )
   
> [!NOTE]
> python3 -m my_own_module test_my_own_module. json
> {"changed": false, "path": "", ""content": "", "invocation": {"module_args": {"path": "testfile.md", "content": "TIPOTOGO"}}}


5. Добавил single task playbook c названием test_playbook.yml и содержимым :  
----
- name: Module testing  
  hosts: localhost  
  tasks:  

  - name: Test module  
    my_own_module:  
      path: './test.txt'  
      content: "Hello world!"  
---
6. Запустил дважды:

1.Первый проход
    
![pr1](https://github.com/user-attachments/assets/612ab151-aa38-4c8c-92c4-e7a227b2fc7f)

2. Второй проход
 
![pr2](https://github.com/user-attachments/assets/e2595019-32ab-445d-aaec-26db5b1ce9b5)


7. Вышел используя **deactivate**
8. Создал новую коллекцию   
	ansible-galaxy collection init my_own_namespace.yandex_cloud_elk  
9. Положил модуль в соответсвующую папку plugins\modules
10. Переделал задачу в роль
11. Создал playbook
12. Выложил коллекцию в гит   
	https://github.com/BelcEV1985/08_ansible_module_06
13. Создал локальный архив из коллекции   
	ansible-galaxy collection build
14. Создал новую директорию test2 и перенёс туда playbook и архив коллекции.
15. Установил коллекцию:  

> [!NOTE]
> **ansible-galaxy collection install -p ansible_collections /test/my_own_collection/my_own_namespace/yandex_cloud_elk/my_own_namespace-yandex_cloud elk-1.0.0.tar.gz**
> 
> Starting galaxy collection install process
>  
> WARNING The specified collections path '/home/testing/ansible/test2/ansible_collections' is not part of the  
> configured Ansible collections paths '/home/testing/.ansible/collections:/usr/share/ansible/collections'. The  
> installed collection will not be picked up in an Ansible run, unless within a playbook-adjacent collections  
> directory.
>   
> Process install dependency map
>  
> Starting collection install process
>   
> Installing 'my_own_namespace.yandex_cloud_elk:1.0.0' to '/home/testing/ansible/test2/ansible_collections/my_own_name  
> namespace/yandex_cloud_elk'
>   
> my_own_namespace.yandex_cloud_elk:1.0.0 was installed successfully  
---------------------
16. Запустил ansible-playbook test_playbook.yml

![pr16](https://github.com/user-attachments/assets/1ef82799-b85e-4da1-b401-e4a2d2547387)

17. [Ссылка на коллекцию](https://github.com/BelcEV1985/08_ansible_module_06)  
    [Ссылка на архив](https://github.com/BelcEV1985/08_ansible_module_06/blob/main/my_own_namespace/yandex_cloud_elk/my_own_namespace-yandex_cloud_elk-1.0.0.tar.gz)
