## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

```sh
$ open https://ngrok.com/
```

## Tasks

- [ ] 1. Ознакомиться со ссылками учебного материала
- [ ] 2. Выполнить инструкцию учебного материала
- [ ] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ cd ~  //переходим в корневую директорию
$ mkdir install //создаем директории
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```

```sh
$ cd tmp
```

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz //скачиваем библиотеку
$ tar -xvzf libevent-2.1.8-stable.tar.gz  //разархивируем
$ cd libevent-2.1.8-stable  // открываем 
$ ./configure --prefix=${HOME_PREFIX} // поиск необходимых для компиляции библиотек и заголовочных файлов.
//он создаст Makefiles - файл, необходимый для сборки программы
// При помощи ключа --prefix=<path> указываем директорию, которая в дальнейшем будет выступать как префикс для нашей программы

$ make && make install // выполняет запуск процедуры компиляции приложения из исходного кода
// и устанавливаем приложение в указанную, на этапе конфигурирования, директорию.

$ cd ..
```

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz
$ tar -xvzf ncurses.tar.gz
$ cd ncurses-5.9
$ ./configure --prefix=${HOME_PREFIX}
$ make && make install
$ cd ..
```


```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
$ tar -xvzf tmux-2.5.tar.gz
$ cd tmux-2.5
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install
$ cd ..
```

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
$ unizp ngrok-stable-linux-amd64.zip
$ mv ngrok ${HOME_PREFIX}/bin //перемещаем ngrok в ${HOME_PREFIX}/bin
```

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib //устанавливаем значение переменных окружения
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux // создаем нулевую сессию (Tmux - позволяет работать с несколькими сессиями в 1 окне.)
```

```sh
$ cd ~
$ rm -rf tmp install // удаляем tmp install
```

```sh
$ brew install tmux ngrok # or use linuxbrew 🎉 //с помощью homebrew устанавливаем ngrok
```

```sh
$ tmux new -s session_with_group  //новая сессия session_with_group
```

```sh
# Alisa:
$ open https://ngrok.com/signup //открываем сайт ngrok
$ export NGROK_TOKEN=<токен>  // экспортируем сгенерированный токен с сайта
$ ngrok authtoken ${NGROK_TOKEN}  // Назначаем уникальный Authtoken, чтобы выявить проблемы, если конкретный Authtoken скомпрометирован.
$ ngrok tcp 22  // запускаем туннель с портом 22 
<порт_ngrok_сервера>
```

```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера> //подкючаем TCP-туннели ngrok к SSH-трафику
<пароль_от_учетной_записи>
$ tmux a -t session_with_group  //подключаемся к уже существующей сессии
$ <C-B>"  //Деление окна горизонтально 
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
