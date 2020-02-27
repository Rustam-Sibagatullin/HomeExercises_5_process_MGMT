# HomeExercises_5_process_MGMT

lsofexample убивает все запущенные процессы опрделенного пользователя, который подключен по ssh.

Принцип работы:
1. выводится список подклченных пользователей: who
2. выбираем пользователя USER_NAME, у которого надо завершить все процессы
3. выводим все подлюченные соединения: sudo lsof -i
4. выводим все открытый файлы пользователя USER_NAME: sudo lsof -u $USER_NAME | more
5. запускаем цикл, который убивает процессы или просто выходит. Цикл не завершается, пока не введен правильный ответ.

while true
do
read -p "Would you like to kill all processes for user? Enter Y(yes) or N(no): " answer

if [[ "$answer" == "Y" ]]; then
    sudo kill -9 `sudo lsof -t -u user2`
    echo "$USER_NAME processes were killed" 
    break
elif [[ "$answer" == "N" ]]; then
    echo "Selected N, USERs proceses will be continie"
    break    
else
    echo
    echo -e "\e[1;31mPlease select correct answer Y(yes) or N(no)\e[0m"
    echo
fi
done

6. после завершиния работы выводим сообщение script finished.


Скрипт полезен при случаях разрыва SSH по вине транспорта, на удаленной машине при этом остаются запущенные процессы.







