
## Основная часть

1. Создайте новый проект в teamcity на основе fork.
2. Сделайте autodetect конфигурации.
3. Сохраните необходимые шаги, запустите первую сборку master.
4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`.

![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/4.PNG)

6. Для deploy будет необходимо загрузить [settings.xml](./teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.
7. В pom.xml необходимо поменять ссылки на репозиторий и nexus.
8. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/5.PNG)

10. Мигрируйте `build configuration` в репозиторий.
11. Создайте отдельную ветку `feature/add_reply` в репозитории.

![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/branch.PNG)

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`.
```
package plaindoll;

public class Welcomer{
	public String sayWelcome() {
		return "Welcome home, good hunter. What is it your desire?";
	}
	public String sayFarewell() {
		return "Farewell, good hunter. May you find your worth in waking world.";
	}
	public String sayNeedGold(){
		return "Not enough gold";
	}
	public String saySome(){
		return "something in the way";
	}
	public String sayHunter() {
		return "The hunter wandered through the taiga for three days.";
  }
}
```
12. Дополните тест для нового метода на поиск слова `hunter` в новой реплике.

```
package plaindoll;

import static org.hamcrest.CoreMatchers.containsString;
import static org.junit.Assert.*;

import org.junit.Test;

public class WelcomerTest {
	
	private Welcomer welcomer = new Welcomer();

	@Test
	public void welcomerSaysWelcome() {
		assertThat(welcomer.sayWelcome(), containsString("Welcome"));
	}
	@Test
	public void welcomerSaysFarewell() {
		assertThat(welcomer.sayFarewell(), containsString("Farewell"));
	}
	@Test
	public void welcomerSaysHunter() {
		assertThat(welcomer.sayWelcome(), containsString("hunter"));
		assertThat(welcomer.sayFarewell(), containsString("hunter"));
	}
	@Test
	public void welcomerSaysSilver(){
		assertThat(welcomer.sayNeedGold(), containsString("gold"));
	}
	@Test
	public void welcomerSaysSomething(){
		assertThat(welcomer.saySome(), containsString("something"));
	}
	@Test
	public void welcomernetSaysHunter(){
		assertThat(welcomer.sayHunter(), containsString("hunter"));
	}
}
```

14. Сделайте push всех изменений в новую ветку репозитория.
15. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.
16. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`.
17. Убедитесь, что нет собранного артефакта в сборке по ветке `master`.
18. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки.
19. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/7.PNG)

21. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.
22. В ответе пришлите ссылку на репозиторий.

---

![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/1.PNG)



![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/2.PNG)



![alt text](https://github.com/stepanovsa061/09-ci-05-teamcity/blob/main/3.PNG)


---

Ссылка на репозиторий: https://github.com/stepanovsa061/example-teamcity
