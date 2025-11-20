# Домашнее задание к занятию 11 «Teamcity»


---

## 1. Виртуальные машины в Yandex Cloud
![yc_vms](img/01.png)
- Три ВМ: TeamCity Server, TeamCity Agent, Nexus.
- Все сервера находятся в одной зоне доступности.

---

## 2. Nexus Repository Manager
![nexus_overview](img/02.png)
- Репозитории `maven-releases`, `maven-snapshots`, `maven-public` настроены.

---

## 3. Сборка TeamCity: `clean test`
![tc_clean_test](img/03.png)
- Первая успешная сборка.
- Запускал только `clean test`.

---

## 4. Логи сборки `clean test`
![tc_clean_test_log](img/04.png)
- Тесты выполняются.
- Артефакты ещё не собираются.

---

## 5. Сборка `clean deploy` + загрузка `settings.xml`
![tc_clean_deploy_with_settings](img/05.png)
- В конфигурацию добавлен шаг `deploy`.
- Загружен корректный `settings.xml` в корень проекта.
- Тест не пройден

---

## 6. Ошибка сборки `clean deploy`
![tc_clean_deploy_error](img/06.png)
### Причина ошибки
Nexus **запрещает перезаписывать артефакты** в `maven-releases`, а версия в `pom.xml` была **одинаковой с уже существующей**.

### Решение
- Повышение версии в `pom.xml` → **0.0.3**.

---

## 7. Успешная сборка `clean deploy`
![tc_clean_deploy_success](img/07.png)
- После увеличения версии публикация прошла успешно.

---

## 8. Логи успешного деплоя
![tc_clean_deploy_success_log](img/08.png)
- Видно, что `.jar` и `.pom` успешно загружены в Nexus.

---

## 9. Артефакт приложения в Nexus
![nexus_artifact](img/09.png)
- Загружен `plaindoll-0.0.3.jar`.

---

## 10. Сборка ветки `feature/add_reply`
![tc_feature_build](img/10.png)
- Сборка триггерится автоматически при `push`.

---

## 11. Логи сборки ветки `feature/add_reply`
![tc_feature_build_log](img/11.png)
- Все тесты прошли.

---

## 12. Обновлённая сборка `master` после merge
![tc_master_build](img/12.png)
- После слияния ветки обновились тесты, и одно новое появилось.

---

## 13. Логи обновлённой сборки `master`
![tc_master_build_log](img/13.png)
- 6 тестов успешно выполнены.

---

## 14. Создание артефактов в TeamCity
![tc_artifacts](img/14.png)
- Добавлены артефакты: оригинальный JAR и shaded JAR.

---

## 15. Артефакты в Nexus после финальной сборки
![nexus_artifacts_final](img/15.png)
- Папка `0.0.3` содержит:
  - `.jar`, `.jar.md5`, `.jar.sha1`
  - `.pom`, `.pom.md5`, `.pom.sha1`
  - `maven-metadata.xml` и контрольные суммы

---

# Репозиторий с Ansible для Nexus
**https://github.com/drumlast/nexus-ansible**

Использовался для автоматической установки и настройки Nexus OSS.

---

# Итог
- Полностью настроена инфраструктура CI/CD.
- TeamCity выполняет тесты, собирает артефакты и публикует их в Nexus.
- Nexus корректно хранит версии и предотвращает перезапись релизов.
- Добавлен новый метод, тест, ветка feature, merge → master.
- Все этапы сопровождаются полным набором логов и скриншотов.

---

