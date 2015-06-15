# BAHomework3
Реализация объектной модели кофе-машины.

Рецепт представлен в виде составного класса Recipe, каждый из компонентов которого
может быть или простым (разрешенным для загрузки в машину) ингредиентом или рецептом.
Для реализации струтуры и общего поведения компонентов рецепта был реализован шаблон "Composite":
    ("Leaf" - Ingredient, "Component" - RecipeComponent, "Composite" - Recipe, "commonOperation" - getIngredient()).

Для создания составных объектов рецептов был использован упрощенный паттерн "Builder"
("Builder" - RecipeBuilder, "Product" - Recipe).

Для создания отдельных компонентов рецепта был реализован паттерн "Factory method"
(AbstractComponentCreator, ComponentCreator, IngredientCreator).

Для хранения данных о рецептах используется шаблон "Repository" (RecipesRepository, LocalRecipesRepository).

Для управления инверсией зависимости был использован DiC Pimple. С его помощью
инициализируются классы- обработчики команд. Инициализация Pimple происходит в файле точки входа cli.php

В качестве текстового интерфейса пользователя была создана простейшая REPL(Read-eval-print loop)-среда,
принимающая команды. Распознавание команд и роутинг производится в классе Application.

Каждую из команд обрабатывает экземпляр отдельного подтипа класса Command.

Для создания исключений созданы классы CLIException, CommandException, RepositoryException, наследующие RuntimeException.
Исключения явно перебрасываются и преобразоваются на каждом уровне.
(Возник вопрос, лучше ли эта практика, чем обработка сразу всех на верхнем уровне обработчиком с несколькими блоками catch).