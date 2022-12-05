# Inleiding
In dit labo gaan we aan de slag met Vagrant. Op het einde van dit labo moet je perfect in staat zijn om vlot met Vragrant te kunnen werken. Alvorens we aan de slag gaan met Vagrant alvast een lijst met bruikbare informatie over Vagrant en hoe je het moet configureren. Bekijk zeker de eerste video, alsook de blog post om een duidelijk begrip te krijgen over Vagrant:

- [Introductie Video](https://www.youtube.com/watch?v=wlogPKBEuUM)
- [Blog Post](https://opensource.com/resources/vagrant)
- Nog meer [clips](https://www.youtube.com/watch?v=a6W1hF9CgDQ) en [clips](https://www.youtube.com/watch?v=sr9pUpSAexE) en nog eens [clips](https://www.youtube.com/watch?v=vBreXjkizgo)
- Een laatste [info](https://ostechnix.com/vagrant-tutorial-getting-started-with-vagrant/)

# Basis
We gaan onze eerste virtuele omgevingen maken.
```
    mkdir vagrant
    cd vagrant
    mkdir debian11
    cd debian11
```
Vanaf hier moeten we een duidelijk verschil maken tussen de provider (= Virtualistatie software) die we gebruiken:
| **VirtualBox** | **VMWare** |
| --- | --- |
|<pre><code>    vagrant init debian/bullseye64</code></pre> | <pre><code>     vagrant init jj-ucll/debian11</code></pre> |

Lees de automatisch aangemaakt Vagrantfile en zorg dat je alle configuratie instellingen begrijpt.

Afhankelijk van welke provider je gebruikt, zal deze file een beetje anders zijn:
| **VirtualBox** | **VMWare** |
| --- | --- |
|<pre><code>config.vm.provider "virtualbox" do \|vb\|</code></pre> | <pre><code>config.vm.provider "vmware_workstation" do \|vb\|</code></pre> |

Start nu de virtuele omgeving en lees aandachtig welke logs er op het scherm verschijnen.
```
    vagrant up
```
Gebruik SSH om in te loggen op de virtuele host. De default gebruiksnaam en wachtwoord is "vagrant" en "vagrant" of "root" en "vagrant" of .... Het is namelijk afhankelijk van het creatie process.
```
    vagrant ssh
```
Wordt root door het volgende commando:
```
    sudo su -
```
Zorg dat de host up to dat is en installeer HTOP
```
    apt-get update
    apt-get upgrade
    apt-get install htop
```
Ga uit de virtuele machine en stop deze.
```
    exit
    vagrant halt
```
Verwijder nu de virtuele machine:
```
    vagrant destroy
```
# Opdrachten

- Default worden de door Vragant opgestarte machine's headless opgestart. Pas de Vagrantfile aan om de GUI (VirtualBox Display of VMWare Display) te laten zien bij het opstarten. Voer volgend commando uit na het aanpassen van de Vagrantfile
  ```
      vagrant reload
  ```
- Pas het aantal voorziene geheugen van de virtuele machine aan naar 2048MB. Voer volgend commando uit na het aanpassen van de Vagrantfile
  ```
      vagrant reload
  ```
- Vragrant heeft standaard een mechanisme ingebouwd om bestanden tussen de host en de VM te delen. Dit noemen ze "Synced folder". Maak een file hello.txt aan in ~/vagrant/debian11. Voeg "Hello World" toe aan de hello.txt file. Pas de Vagrantfile aan om de directory dat de Vagrantfile bevat te syncen naar /vagrant op de VM.
  ```
      config.vm.synced_folder ".", "/vagrant", disabled: false
  ```
  
  ❗Let op, bij VMWare lijkt het alsof dit niet gelukt is (df zal de mount niet laten zien) echter het is er wel. Probeer maar eens naar /vagrant te gaan. It's not a bug, it's a FEATURE.
  
  Voer daarna volgende commando uit:
  ```
      vagrant reload
  ```
- Leg in detail uit wat de volgende commando's doen:
  ```
      vagrant suspend

      vagrant status
      
      vagrant resume
  ```
- De Vagrantfile bevat details van de virtuele omgeving. Gebruik de volgende code om een lege file (hello.txt) aan te maken in /tmp van de vm virtual environment/machines.
  ```
        config.vm.provision "shell", inline: <<-SHELL
            touch /tmp/hello.txt
        SHELL
  ```
  Ga na of de file wordt aangemaakt door de VM te verwijderen en terug aan te maken. Log in op de VM via vagrant ssh. Gebruik het commando "id" om na te gaan wat je indentiteit is. Dit zou "vagrant" moeten zijn. Ga ook na wie de eigenaar is van /tmp/hello.txt. Dit zou "root" moeten zijn. Hiermee kunnen we besluiten dat Vragrant de mogelijkheid heeft om root te worden op de VM en dus ook als root commando's kan uitvoeren.
- Wijzig de naam van de VM, naar je eigen naam.
- Gebruik de SHELL provisioner op apache2 te installeren.
  ```
   config.vm.provision "shell", inline: <<-SHELL
       apt update -y
       apt upgrade -y
       apt install apache2 -y
       service apache2 status
   SHELL
   ```
- Forward tcp poort 8384 op je eigen computer naar poort 80 op de VM en ga na of deze portfoward werkt. Normaal zou je dan de standaard apache webpagina moeten zien.
