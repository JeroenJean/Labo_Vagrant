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
Vanaf hier moeten we een duidelijk verschil maken tussen de provider die we gebruiken:
| **VirtualBox** | **VMWare** |
| --- | --- |
|<pre><code>    vagrant init debian/bullseye64</code></pre> | <pre><code>     vagrant init jj-ucll/debian11</code></pre> |

Lees de automatisch aangemaakt Vagrantfile en zorg dat je alle configuratie instellingen begrijpt.\\\\
Start nu de virtuele omgeving en lees aandachtig welke logs er op het scherm verschijnen.
\begin{verbatim}
    vagrant up
\end{verbatim}
Gebruik SSH om in te loggen op de virtuele host. De default gebruiksnaam en wachtwoord is "vagrant" en "vagrant" of "root" en "vagrant" of .... Het is namelijk afhankelijk van het createi process.
\begin{verbatim}
    vagrant ssh
\end{verbatim}
Wordt root door het volgende commando:
\begin{verbatim}
    sudo su -
\end{verbatim}
Zorg dat de host up to dat is en installeer HTOP
\begin{verbatim}
    apt-get update
    apt-get upgrade
    apt-get install htop
\end{verbatim}
Ga uit de virtuele machine en stop deze.
\begin{verbatim}
    exit
    vagrant halt
\end{verbatim}
Verwijder nu de virtuele machine:
\begin{verbatim}
    vagrant destroy
\end{verbatim}
