5. Какие ресурсы выделены по-умолчанию?  
```
Оперетивная память: 1024 МБ
Процессоры: 2
Видеопамять: 4 МБ
Носители: 64 ГБ
```


6. Как добавить оперативной памяти или ресурсов процессора виртуальной машине?
```
Vagrant.configure("2") do |config|
 	config.vm.box = "bento/ubuntu-20.04"
 	config.vm.provider "virtualbox" do |v|
 	  v.memory = 2048
 	  v.cpus = 3nn
 	end
end
```


8. какой переменной можно задать длину журнала history, и на какой строчке manual это описывается?  
```
bash(1) HISTFILESIZE (line 1137) - максимальное число строк в файле истории
bash(1) HISTSIZE (line 1160) - число команд для сохранения
```

_что делает директива ignoreboth в bash?_    

```
bash (1) line 1122 (man bash -> /ignore -> дальше листал документацию n n n...

A value of ignoreboth is shorthand for ignorespace and ignoredups. 

ignoreboth это сокращение для 2х директив ignorespace and ignoredups, 
    ignorespace - не сохранять команды начинающиеся с пробела, 
    ignoredups - не сохранять команду, если такая уже имеется в истории
```

9. В каких сценариях использования применимы скобки {} и на какой строчке man bash это описано?

```
man bash -> "/\{" (первый и второй результат)
строка 234
       RESERVED WORDS
       Reserved words are words that have a special meaning to the shell.   The
       following  words are recognized as reserved when unquoted and either the
       first word of a simple command (see SHELL GRAMMAR below)  or  the  third
       word of a case or for command:

       ! case  coproc  do done elif else esac fi for function if in select then
       until while { } time [[ ]]
	   
строка 338
		{ list; }
              list  is  simply executed in the current shell environment.  list
              must be terminated with a newline or semicolon.  This is known as
              a  group  command.  The return status is the exit status of list.
              Note that unlike the metacharacters ( and ), { and } are reserved
              words  and  must  occur  where a reserved word is permitted to be
              recognized.  Since they do not cause a word break, they  must  be
              separated from list by whitespace or another shell metacharacter.

{} - зарезервированные слова, список, в т.ч. список команд команд в отличии от "(...)" исполнятся в текущем инстансе, 
используется в различных условных циклах, условных операторах, или ограничивает тело функции, 
В командах выполняет подстановку элементов из списка , если упрощенно то  цикличное выполнение команд с подстановкой 
например mkdir ./DIR_{A..Z} - создаст каталоги сименами DIR_A, DIR_B и т.д. до DIR_Z
```


10. С учётом ответа на предыдущий вопрос, как создать однократным вызовом touch 100000 файлов? Получится ли аналогичным образом создать 300000? Если нет, то почему?

```

touch {000001..100000} работает, создано 100000 файлов

touch {000001..100000} не работает, ошибка -bash: /usr/bin/touch: Argument list too long


```

11. В man bash поищите по /\[\[. Что делает конструкция [[ -d /tmp ]]

```
       [[ expression ]]
              Return a status of 0 or 1 depending on the evaluation of the conditional expression expression.  Expressions  are  com‐
              posed  of  the  primaries described below under CONDITIONAL EXPRESSIONS.  Word splitting and pathname expansion are not
              performed on the words between the [[ and ]]; tilde expansion, parameter and variable expansion, arithmetic  expansion,
              command  substitution, process substitution, and quote removal are performed.  Conditional operators such as -f must be
              unquoted to be recognized as primaries.

              When used with [[, the < and > operators sort lexicographically using the current locale.

		 -d file
					  True if file exists and is a directory.
					  
проверяет условие у -d /tmp и возвращает ее статус (0 или 1), (наличие катаолга /tmp)


```



12. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе 

Команды:  
```
vagrant@vagrant:~$ mkdir /tmp/new_path_dir/
vagrant@vagrant:~$ cp /bin/bash /tmp/new_path_dir/
vagrant@vagrant:~$ type -a bash
bash is /usr/bin/bash
bash is /bin/bash
vagrant@vagrant:~$ PATH=/tmp/new_path_dir/:$PATH
vagrant@vagrant:~$ type -a bash
bash is /tmp/new_path_dir/bash
bash is /usr/bin/bash
bash is /bin/bash
```

13. Чем отличается планирование команд с помощью batch и at?

```
at - команда запускается в указанное время
batch - запускается когда уровень загрузки системы снизится ниже 1.5
```


14. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.

```
vagrant suspend
vagrant halt
```
