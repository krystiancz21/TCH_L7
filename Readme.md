# LAB7 - Sprawozdanie

Repozytorium zawiera plik Dockerfile oraz skrypty umożliwiające zbudowanie obrazu Dockera, który działa na różnych architekturach procesorów (amd64, arm64). Wymagane jest użycie narzędzi Docker Buildx oraz multiarch/qemu-user-static, które umożliwiają budowanie i uruchamianie obrazów na różnych platformach.

Przebieg zadania:
* Stworzenie nowego buildera: docker buildx create labbuilder 
* Ustawienie nowego buildera: docker buildx use labbuilder
* Sprawdzenie konfiguracji Buildx: docker buildx inspect --bootstrap
* Ustawienie wirtualnego środowiska wykonawczego dla platform, które nie odpowiadają bieżącej architekturze procesora:
  docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
* Budowanie obrazu dla platformy amd64 oraz arm64 (screen: L7cz1.png):
  docker buildx build -t docker.io/s95382/labo7:zad1 --platform linux/amd64,linux/arm64 --push .

* Repozytorium DockerHub z obrazem: https://hub.docker.com/r/s95382/labo7/tags

* Pobranie obrazu z repozytorium (screen: L7cz2.png): docker pull s95382/labo7:zad1
* Uruchomienie kontenera na podstawie pobranego obrazu (screen: L7cz2.png): 
  docker run -d -p 80:80 --name lab7app s95382/labo7:zad1
* Sprawdzenie czy kontener działa (screen: L7cz2.png): docker ps
* Wyświetlenie zawartości strony z nazwiskiem autora (screen: L7cz2.png): curl localhost:80

* Wyświetlenie zawartości manifestu (screen: L7cz3.png): docker buildx imagetools inspect s95382/labo7:zad1