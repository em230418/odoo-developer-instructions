================================
 Настройка окружения для работы
================================

Выбор ОС
========

Предполагается, что у разработчика установлена ОС на базе Linux.
Если Вы достаточно хорошо знакомы с подобными ОС, то этот раздел можно пропустить.

Для начинающих пользователей подобных ОС, самый подходящий вариант - это Linux Mint.
На момент написания этих строк, эта ОС распространяется в 4-х вариантах.
Предлагается использовать `Linux Mint с рабочим окружением Xfce <https://linuxmint.com/edition.php?id=286>`__.

Данный раздел не будет затрагивать процесс установки данной ОС.
При возникновении вопросов по процессу установки, свяжитесь с ведущим разработчиком.

О терминале
===========

Под терминалом можно назвать аналог интерпретатора командой строки в Windows (cmd.exe).
В процессе работы он очень часто используется.

Везде, где говорится "выполните эту команду", подразумевается открыть терминал и ввести туда указанную команду.

Настройка путей и переменных окружения
======================================

Предполагается, что все для работы будет находиться в каталоге ``/opt``.

Создаем каталог ``/opt`` и устанавливаем владельца этого каталога на текущего пользователя.

.. code-block:: sh

   sudo mkdir /opt
   sudo chown $USER:$USER /opt

Также создаем каталог ``/opt/bin`` в котором будут храняться исполняемые файлы или символические ссылки на исполняемые файлы.

.. code-block:: sh

   mkdir /opt/bin

Этот каталог надо добавить в переменную окружения PATH. Для этого в файле ~/.bashrc в самом конце добавляем следующую строку:

   export PATH=/opt/bin:$PATH

И перезапустите терминал.


Установка программ
==================

Для работы необходимо установить:

1. систему контроля версий git
2. интерпретатор Python 3
3. утилиту для создании виртуальных окружений
4. Docker
5. docker-compose

Для установки первых трех выполните следующую команду:

.. code-block:: sh

    sudo apt-get update
    sudo apt-get install git python3 python3-venv

Установка docker-compose
------------------------

..
     Основано на https://docs.docker.com/compose/install/

Для установки docker-compose выполните по-очередно следующие команды:

.. code-block:: sh

     sudo curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /opt/bin/docker-compose
     sudo chmod +x /opt/bin/docker-compose

Для проверки работоспособности убедитесь, что следующая команда выведет версию

.. code-block:: sh

     docker-compose --version

Установка Docker
----------------

..
    Основано на https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

Для установки Docker выполните по-очередно следующие команды:

.. code-block:: sh

    sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    echo \
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io

Чтобы убедиться, что Docker успешно установлен и работает, выполните следующую команду:

.. code-block:: sh

    sudo docker run hello-world

В случае успеха вернет многобукав среди которых будет "Hello from Docker!".

Напоследок, чтобы была возможность выполнять команды docker и docker-compose без sudo:

1. выполните следующую команду:

.. code-block:: sh

    sudo usermod -aG docker $USER

2. перелогинтесь
3. проверьте, что следующая команда не выведет что-то на подобии Permission denied

.. code-block:: sh

   docker run hello-world

Установка PyCharm
-----------------

Если какое-либо приложение требует установки в обход метода ``sudo apt-get install``, то практикуется установка в данный каталог.
Среди подобных приложения является PyCharm.

Переходим в данный каталог и уставливаем PyCharm:

.. code-block:: sh

   cd /opt
   wget https://download-cf.jetbrains.com/python/pycharm-community-2020.3.5.tar.gz -O pycharm-community.tar.gz
   tar xvf pycharm-community.tar.gz
   mv pycharm-community-2020.3.5 pycharm-ce
   ln -s /opt/pycharm-ce/bin/pycharm.sh /opt/bin/pycharm


Далее создаем символическую ссылку на рабочем столе (опционально):

.. code-block:: sh

   cd ~/Desktop
   # каталог с рабочим столом может называться также "Рабочий стол"
   # если команда выше не сработает, то выполните следующую команду
   cd ~/Рабочий\ стол
   ln -s /opt/bin/pycharm pycharm

Установка шаблонизатора
-----------------------

TODO:

Настройка виртуальных окружений
===============================

TODO: https://github.com/em230418/docker-odoo
