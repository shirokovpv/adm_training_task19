# adm_training_task19
<h1 align="center">Занятие 19. Разворачиваем сетевую лабораторию</h1>
<ol>
<li><span style="font-weight: 400;">Развернуть Vagrant-стенд&nbsp;</span></li>
<li><span style="font-weight: 400;"> Построить следующую сетевую архитектуру:</span></li>
</ol>
<p><span style="font-weight: 400;">Сеть office1</span></p>
<p><span style="font-weight: 400;">- 192.168.2.0/26&nbsp; &nbsp; &nbsp; - dev</span></p>
<p><span style="font-weight: 400;">- 192.168.2.64/26 &nbsp; &nbsp; - test servers</span></p>
<p><span style="font-weight: 400;">- 192.168.2.128/26&nbsp; &nbsp; - managers</span></p>
<p><span style="font-weight: 400;">- 192.168.2.192/26&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">Сеть office2</span></p>
<p><span style="font-weight: 400;">- 192.168.1.0/25&nbsp; &nbsp; &nbsp; - dev</span></p>
<p><span style="font-weight: 400;">- 192.168.1.128/26&nbsp; &nbsp; - test servers</span></p>
<p><span style="font-weight: 400;">- 192.168.1.192/26&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">Сеть central</span></p>
<p><span style="font-weight: 400;">- 192.168.0.0/28 &nbsp; &nbsp; - directors</span></p>
<p><span style="font-weight: 400;">- 192.168.0.32/28&nbsp; &nbsp; - office hardware</span></p>
<p><span style="font-weight: 400;">- 192.168.0.64/26&nbsp; &nbsp; - wifi</span></p>
<p><span style="font-weight: 400;">Итого должны получиться следующие сервера:</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">inetRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">centralRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office1Router</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office2Router</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">centralServer</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office1Server</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">office2Server</span></li>
</ul>
<p><span style="font-weight: 400;">В практической части требуется:&nbsp;</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">Соединить офисы в сеть согласно логической схеме и настроить роутинг</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Интернет-трафик со всех серверов должен ходить через inetRouter</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Все сервера должны видеть друг друга (должен проходить ping)</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">У всех новых серверов отключить дефолт на NAT (eth0), который vagrant поднимает для связи</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Добавить дополнительные сетевые интерфейсы, если потребуется</span></li>
</ul>
<h3 class="western"><a name="_heading=h.df570rpzx1qg"></a><span style="font-family: Roboto, serif;"><span style="font-size: small;">Используемые ОС</span></span></h3>
<p style="line-height: 108%; margin-bottom: 0.28cm;" align="justify"><span style="font-family: Roboto, serif;">Хостовая ОС Ubuntu 24.04 Desktop с установленным Vagrant 2.3.5. VirtualBox версия 7.0.16_Ubuntu r162802</span></span></p>
<h3 class="western"><span style="font-family: Roboto, serif;"><span style="font-size: small;">Выполнение</span></span></h3>
<p>******************************</p>
<p>Ввиду невозможности в нынешних реалиях воспользоваться стандартными репозиториями Vagrant (в РФ они сейчас не доступны), предложено обходное решение. Использован репозиторий, развернутый на&nbsp;<a href="https://vagrant.elab.pro/" rel="nofollow">https://vagrant.elab.pro/</a></p>
<p>Так как официальный пакет последней версии Vagrant также не доступен для скачивания, пакет взят оттуда же. Версия 2.3.5.</p>
<img width="411" height="88" alt="image" src="https://github.com/user-attachments/assets/7591c684-f543-4bf6-bfa8-3706a7648c97" />
<p>&nbsp;</p>
<p>Для подключения репозитория надо добавить в Vagrant-файл строку:</p>
<p><code>ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'</code></p>
<p>И изменить box_name и box_version (как в репозитории, если туда зайти).</p>
<img width="272" height="153" alt="image" src="https://github.com/user-attachments/assets/8a216a0c-b904-48e5-aa78-bd21d80e3052" />
<p>******************************</p>
<p>Создаем каталог ~/task19, а в нем Vagrantfile для развертывания виртуальных машин. Скачаем Vagrantfile из репозитория https://github.com/erlong15/otus-linux/tree/network
и изменим его в соответствии с заданием и обходным решением, описанным выше. ОС Ubuntu 22.04, добавляем новые хосты и сетевые настройки для хостов. Измененный файл прикладываю сюда.</p>
<p>После выполнения команды <code>vagrant up</code> получим 7 виртуальных машин.</p>
<img width="1089" height="562" alt="image" src="https://github.com/user-attachments/assets/6dfede39-7dc0-4f82-a807-149d5c8b3b4b" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">После того, как все 7 серверов у нас развернуты, нам нужно настроить маршрутизацию и NAT таким образом, чтобы доступ в Интернет со всех хостов был через inetRouter и каждый сервер должен быть доступен с любого из 7 хостов.</span></p>
<p><strong>Настройка NAT</strong></p>
<p><span style="font-weight: 400;">1) Подключимся по SSH к хосту inetRouter:</p>
<p><span style="font-weight: 400;"><code>vagrant ssh inetRouter</code></p>
<p><span style="font-weight: 400;"><code>sudo -i</code></p>
<p><span style="font-weight: 400;">2) Проверим, включен ли файервол: <code>systemctl status ufw</code></p>
<img width="715" height="210" alt="image" src="https://github.com/user-attachments/assets/529f8473-6179-4148-b828-2c86d2939370" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">Останавливаем и отключаем:</span></p>
<p><code>systemctl stop ufw</code></p>
<p><code>systemctl disable ufw</code></p>
<img width="812" height="118" alt="image" src="https://github.com/user-attachments/assets/e022d068-ff5e-4f07-8220-040116873009" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">3) Создаём файл <strong>/etc/iptables_rules.ipv4</strong></p>
<p><code>nano /etc/iptables_rules.ipv4</code></p>
<p>*filter<br />:INPUT ACCEPT [90:8713]<br />:FORWARD ACCEPT [0:0]<br />:OUTPUT ACCEPT [54:7429]<br />-A INPUT -p icmp -j ACCEPT<br />-A INPUT -i lo -j ACCEPT<br />-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT<br />COMMIT</p>
<p>*nat<br />:PREROUTING ACCEPT [1:44]<br />:INPUT ACCEPT [1:44]<br />:OUTPUT ACCEPT [0:0]<br />:POSTROUTING ACCEPT [0:0]<br />-A POSTROUTING ! -d 192.168.0.0/16 -o eth0 -j MASQUERADE<br />COMMIT</p>
<img width="540" height="331" alt="image" src="https://github.com/user-attachments/assets/fa1903d2-ff0e-4c2d-832a-372833ac5ae1" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">4) Создаём файл, в который добавим скрипт автоматического восстановления правил при перезапуске системы:</span></p>
<p><code>nano /etc/network/if-pre-up.d/iptables</code></p>
