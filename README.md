# Домашнее задание к занятию 11 «`Teamcity`» -  `Живарев Игорь`

## Подготовка к выполнению

1. В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`.
2. Дождитесь запуска teamcity, выполните первоначальную настройку.
3. Создайте ещё один инстанс (2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему переменную окружения `SERVER_URL: "http://<teamcity_url>:8111"`.
4. Авторизуйте агент.
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity).
6. Создайте VM (2CPU4RAM) и запустите [playbook](./infrastructure).

## Основная часть

1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.
3. Сохраните необходимые шаги, запустите первую сборку master.
4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.
5. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
6. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.
8. Мигрируйте `build configuration` в репозиторий.
9. Создайте отдельную ветку `feature/add_reply` в репозитории.
10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.
11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.
12. Сделайте push всех изменений в новую ветку репозитория.
13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
15. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
19. В ответе пришлите ссылку на репозиторий.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---




### Ответы


Создынные VM в Yandex.Cloud

![yandex](img/ci-05_01.png)


Выполнение 'playbook', создание сервера 'Nexus'

![playbook](img/ci-05_02.png)


Сделайте autodetect конфигурации

![autodetect](img/ci-05_03.png)


Запуск первой сборки 'master'

![master](img/ci-05_04.png)


Поменяйте условия сборки: если сборка по ветке 'master', то должен происходит 'mvn clean deploy', иначе 'mvn clean test'

![mvn](img/ci-05_05.png)


Загрузить 'settings.xml' в набор конфигураций maven

![settings.xml](img/ci-05_06.png)


Всё прошло успешно и артефакт появился в nexus

![nexus](img/ci-05_07.png)


Миграция 'build configuration' в репозиторий

![build](img/ci-05_08.png)


Тесты из ветки 'feature/add_reply' прошли успешно 

![nexus](img/ci-05_09.png)


Внесение изменений из произвольной ветки 'feature/add_reply' в 'master' через Merge:

```
╭─shaman@Barton ~/git_netology/example-teamcity ‹feature/add_reply› 
╰─$ git checkout main
Переключено на ветку «main»
Ваша ветка обновлена в соответствии с «origin/main».
╭─shaman@Barton ~/git_netology/example-teamcity ‹main› 
╰─$ git merge feature/add_reply
Обновление 5fec707..e7b8341
Fast-forward
 .teamcity/Netology/buildTypes/Netology_Build.xml                                         |  60 ++++++++++
 .teamcity/Netology/pluginData/mavenSettings/settings.xml                                 | 261 +++++++++++++++++++++++++++++++++++++++++++
 .teamcity/Netology/project-config.xml                                                    |  19 ++++
 .../Netology/vcsRoots/Netology_HttpsGithubComZhivarevExampleTeamcityGitRefsHeadsMain.xml |  17 +++
 pom.xml                                                                                  |   2 +-
 src/main/java/plaindoll/Welcomer.java                                                    |   3 +
 src/test/java/plaindoll/WelcomerTest.java                                                |   3 +-
 7 files changed, 363 insertions(+), 2 deletions(-)
 create mode 100644 .teamcity/Netology/buildTypes/Netology_Build.xml
 create mode 100644 .teamcity/Netology/pluginData/mavenSettings/settings.xml
 create mode 100644 .teamcity/Netology/project-config.xml
 create mode 100644 .teamcity/Netology/vcsRoots/Netology_HttpsGithubComZhivarevExampleTeamcityGitRefsHeadsMain.xml
```

Проверка повторной сборки мастера, сборка прошла успешно и артефакты собраны.

![игшдв-02](img/ci-05_10.png)

![nexus-03](img/ci-05_11.png)

---

