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

Установка программ
==================

Для работы необходимо установить:

1. систему контроля версий git
2. интерпретатор Python 3
3. утилиту для создании виртуальных окружений
4. Docker
5. docker-compose

Для установки первых трех в терминале выполните следующую команду:

.. code-block:: sh

    sudo apt-get update
    sudo apt-get install git python3 python3-venv

Установка docker-compose
------------------------

..
     Основано на https://docs.docker.com/compose/install/

Для установки docker-compose выполните по-очередно следующие команды:

.. code-block:: sh

     sudo curl -L "https://github.com/docker/compose/releases/download/1.28.6/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

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
