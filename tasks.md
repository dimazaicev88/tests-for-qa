
Тест расчитан на  понимания основого принципа работы таких фреймворком как Selenium,MyIbatis,Spring AOP. Время выполнения ~30 минут.

Задание 1:
Используя Java Dynamic Proxy (https://docs.oracle.com/javase/8/docs/technotes/guides/reflection/proxy.html)
реализуйте метод
 ``` java
 MainPage createPage(Class clazz),
 ```
класса MethodInterception, таким образом что бы проходил тест:
``` java

@Retention(java.lang.annotation.RetentionPolicy.RUNTIME)
@Target({METHOD, TYPE})
public @interface Selector {

    String xpath();
}

public interface MainPage {

    @Selector(xpath = ".//*[@test-attr='input_search']")
    String textInputSearch();

    @Selector(xpath = ".//*[@test-attr='button_search']")
    String buttonSearch();
}

public class MethodInterception {

    @Test
    public void annotationValue() {
        MainPage mainPage = createPage(MainPage.class);
        assertNotNull(mainPage);
        assertEquals(mainPage.buttonSearch(), ".//*[@test-attr='button_search']");
        assertEquals(mainPage.textInputSearch(), ".//*[@test-attr='input_search']");
    }

    private MainPage createPage(Class clazz) {
        return null;
    }
}
```

