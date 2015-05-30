# Installation instructions (Win32) #

Автор: **bookwarrior**
Добавлено: Пн авг 31, 2009 12:00 pm (ред. Май 2014)
[Форум LibGen](http://genofond.org/viewtopic.php?p=3575#p3575)


руководство архивом
> [LibraryGenesis-Win32-manual.rar](https://lgsoft-developers-libgen.googlecode.com/files/LibraryGenesis-Win32-manual.rar) [102.64 Кб]


<br>
<font color='brown' size='5' face='Arial'>Чистая установка</font>
<br>

"Чистая" значит убрать предыдущие инсталляции <b>Apache HTTP Server</b>, <b>PHP</b> и <b>MySQL Server</b>, выключить все серверы, которые есть на компьютере, сетевые программы, которые работают в режиме сервера и могут использовать порт 80: обязательно выключить <b>Skype</b>, мессенджеры и разнообразные ослы.<br>
<br>
<br>
<font color='brown' size='5' face='Arial'>Необходимые компоненты</font>
<br>

Это полный набор необходимых компонент - ничего больше не требуется для запуска кода. Всё следует выкачать перед началом установки.<br>
<br>
<ul><li><a href='https://drive.google.com/file/d/0BwjOuMhpEDpQOG81NzhoMm9aRkE/edit?usp=sharing'>MySQL Server 5.1.45 и выше</a>, (45 MB)<br>
</li><li><a href='https://lgsoft-developers-libgen.googlecode.com/files/php-5.2.5-win32-installer.msi'>PHP 5.2.5</a>, (19.3 MB)<br>
</li><li><a href='https://lgsoft-developers-libgen.googlecode.com/files/apache_2.2.8-win32-x86-no_ssl.msi'>Apache HTTP Server 2.2.8</a>, (4.17 MB)<br>
</li><li>Последний дамп базы данных, качать с <a href='ftp://libgen.org/dbdumps'>фтп Libgen</a> или с <a href='http://gen.lib.rus.ec/'>лицевой страницы</a> (линк <b>Dump</b>).<br>
</li><li>Последние исходники сайта, тоже с главной, линк <b>Code</b>.</li></ul>

<br>
<font color='brown' size='5' face='Arial'>Установка MySQL Server</font>
<br>

<ol><li>Запустить инсталлятор и соглашаться со всеми настройками, пока не увидите окно выбора конфигурации:<br><img src='https://lgsoft-developers-libgen.googlecode.com/files/wiki_Installation_instructions_Win32_1.jpg' /><br>
</li><li>Жмём Next:<br><img src='http://wiki.lgsoft-developers-libgen.googlecode.com/git/images/wiki_Installation_instructions_Win32_2_2.jpg' /><br>
</li><li>Выберите пароль для пользователя root, повторив его дважды. Далее он будет нужен для модификации файла config.php из кода сайта:<br><img src='https://lgsoft-developers-libgen.googlecode.com/files/wiki_Installation_instructions_Win32_3.jpg' /><br>
</li><li>Жмём Execute:<br><img src='https://lgsoft-developers-libgen.googlecode.com/files/wiki_Installation_instructions_Win32_4.jpg' /><br>
</li><li>Если всё хорошо, последнее окно выглядит так:<br><img src='https://lgsoft-developers-libgen.googlecode.com/files/wiki_Installation_instructions_Win32_5.jpg' /><br></li></ol>

<br>
<font color='brown' size='5' face='Arial'>Установка базы данных Library Genesis</font>
<br>

<ol><li>Распаковать дамп базы данных (напр., файл <b>bookwarrior.updated 20090830 1449.rar</b>);<br>(libgen_dbbackup-last.rar - последний актуальный дамп, только основные таблицы, бекапится ежедневно,<br>libgen_dbbackup-[yyy-mm-dd-hh-mm].rar - дамп за указанную дату, только основные таблицы, бекапится ежедневно<br>libgen_dbbackup-last-all-[yyy-mm-dd-hh-mm].rar - полный дамп за указанную дату, бекапится еженедельно)<br>
</li><li>В командной строке вводим, если базу установили без пароля:<br>
<pre><code>Код:<br>
<br>
mysql -u root<br>
create database bookwarrior;<br>
quit<br>
mysql -u root -D bookwarrior &lt; "C:\backup_ba.sql"<br>
</code></pre>
либо, если установили пароль на юзера root в базе<br>
<pre><code>Код:<br>
<br>
mysql -u root -p<br>
create database bookwarrior;<br>
quit<br>
mysql -u root -p -D bookwarrior &lt; "C:\backup_ba.sql"<br>
</code></pre></li></ol>


<br>
<font color='brown' size='5' face='Arial'>Установка Web-сервера, PHP и кода сайта</font>
<br>

<ol><li>Ставим <b>Apache HTTP Server</b>, без фокусов - только кнопки Next/OK; после инсталляции <b>Apache</b> сам уже будет запущен;<br>
</li><li>Останавливаем <b>Apache</b> (чтобы освободить httpd.conf для редактирования инсталлятором PHP дальше);<br>
</li><li>Изменяем <b>AllowOverride None</b> на <b>AllowOverride All</b> в "C:\Program Files\Apache Software Foundation\Apache2.2\conf\<b>httpd.conf</b>" в секции <Directory "C:/Program Files/Apache Software Foundation/Apache2.2/htdocs">;<br>
</li><li>Ставим <b>PHP</b>. По ходу инсталляции выбираем последовательно:<br> а) Apache 2.2.x Module;<br> б) C:\Program Files\Apache Software Foundation\Apache2.2\conf\<br> в) Extensions: MySQL;<br>
</li><li>Запускаем <b>Apache</b>;<br>
</li><li>Распаковываем исходники сайта <b>(gen.lib.rus.ec.7z)</b> в каталог "C:\Program Files\Apache Software Foundation\Apache2.2\htdocs\", старое содержимое этого каталога можно удалить;<br>
</li><li>Редактируем <b>config.php</b>: записываем<br>
<pre><code>Код:<br>
<br>
$dbuser = 'root';<br>
$dbpass = 'пароль, введённый для MySQL Server ранее';<br>
</code></pre>
</li><li>Проверяем через <a href='http://localhost/'>http://localhost/</a> Результатом должна быть страница поиска Library Genesis.</li></ol>

Прикрепляю конфигурационный файл <b>Apache</b> httpd.conf для настроек по умолчанию плюс указанные выше правки. Должен работать, если Apache и PHP установлены в каталоги по умолчанию и взяты на либгене.<br>
<br>
<blockquote><a href='https://lgsoft-developers-libgen.googlecode.com/files/httpd.conf.rar'>httpd.conf.rar</a> [4.9 Кб]</blockquote>

<br>
<font color='brown' size='5' face='Arial'>Ремарки</font>
<br>

<ul><li>Иногда бывает нужно перезагрузиться, если приходилось удалять софт и повторять установку заново. Особенно это касается сервера MySQL: постарайтесь всё сделать с первого раза, чтобы не приходилось много раз очищаться и перезагружаться в последствии.<br>
</li><li>Проделал описанное несколько раз на чистой машине - работает. Расход времени на всё - 15 минут.<br>
</li><li>Файлы книг скачиваются независимо от кода и для его функционирования не требуются. По мере скачивания репозитория, подкладывайте новые подпапки в "C:\Program Files\Apache Software Foundation\Apache2.2\htdocs\<b>repository</b>\" - это ваш репозиторий. Сколько будет файлов - столько книг локальный Library Genesis сможет вам отдать. В случае, если книги ещё нет, просто скажет, что её нет, но в поиске она будет присутствовать, потому что присутствует в базе данных.<br>
</li><li>Каталог инсталляции Apache можете выбрать произвольный - в примере взят каталог по умолчанию для простоты.<br>
</li><li>Можно изменить расположение каталога с веб-сайтом на более удобное двумя следующими заменами в <b>httpd.conf</b> (лучше тогда сохранить обе копии httpd.conf, чтобы удобно переключать):<br>
<pre><code>Код:<br>
<br>
#DocumentRoot "C:/Program Files/Apache Software Foundation/Apache2.2/htdocs"<br>
DocumentRoot "h:/www"<br>
</code></pre>
<pre><code>Код:<br>
<br>
#&lt;Directory "C:/Program Files/Apache Software Foundation/Apache2.2/htdocs"<br>
Directory "h:/www"<br>
</code></pre>
После редактирования перезапустить Apache.