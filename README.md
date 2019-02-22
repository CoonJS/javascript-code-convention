# code-conventions

Code concepts, principles and examples for large long term projects

# Содержание
  1. [Введение](#Введение)
  2. [Ценности](#Ценности)
  3. [Принципы](#Принципы)
  4. [Общие правила](#Общие_правила)
  5. [Работа с переменными](#Работа_с_переменными) 
  6. [Логические переменные и методы](#Логические_переменные_и_методы) 
  7. [Работа с методами](#Работа_с_методами) 
  8. [Возврат результата работы метода](#Возврат_результата_работы_метода) 
  9. [Работа с объектами](#Работа_с_объектами) 
  10. [Комментирование кода](#Комментирование_кода) 
  11. [Особенности Pull/Merge Request (PR | MR)](#Особенности_Pull/Merge_Request) 
  12. [Работа с условиями](#Работа_с_условиями) 
  13. [Работа с тернарными операторами](#Работа_с_тернарными_операторами) 
  14. [Работа с React компонентами](#Работа_с_react_компонентами)
  
  **Введение**
  
  Этот документ содержит правила написания кода (Code Conventions) в [компании BiZone](https://www.bi.zone/). 
  
  Здесь всегда будет находится актуальная версия нашего Code Conv, так как мы будем ссылаемся на него при проведении наших Code Review.
  
  Code Conv — это правила, которые нужно соблюдать при написании любого кода. Мы различаем Code Style и Code Conv. Для нас Code Style — это внешний вид кода. То есть расстановка отступов, запятых, скобок и прочего. А Code Conv — это смысловое содержание кода. Правильные алгоритмы действий, правильные по смыслу названия переменных и методов, правильная композиция кода. Соблюдение Code Style легко проверяется автоматикой. А вот проверить соблюдение Code Conv в большинстве случаев может только человек.
  
  **Ценности**
  
  Главная цель Code Conv — сохранение низкой стоимости разработки и поддержки кода на длинной дистанции.
  
  Основные ценности, помогающие достичь этой цели:
  
  ***Читаемость***
  
  Код должен легко читаться, а не легко записываться. Это значит, что такие вещи как синтаксический сахар (если он направлен на ускорение записи, а не дальнейшего чтения кода) вредны.
  Обратите внимание, что быстродействие кода не является ценностью, поэтому не самый оптимальный цикл, но удобный для понимания, будет лучше, чем быстрый, но сложный. Не нужно экономить переменные, буквы для их названий, оперативную память и так далее.
  
  ***Вандалоустойчивость***
  
  Код надо писать так, чтобы у разработчика, который с ним будет работать, было как можно меньше возможности внести ошибку. Например, покрывайте тестами не только краевые условия, но и кейсы, которые могут появиться в результате доработок кода и рефакторинга.
  
  ***Поддержание наименьшей энтропии***
  
  Энтропия — это количество информации, из которой состоит проект (информационная емкость проекта). Код проекта должен выполнять продуктовые требования с сохранением наименьшей возможной энтропии.
  
  **Принципы**
  
  Принципы — это способы соблюдения описанных выше ценностей. Они чуть более детальны, содержат основные методологии разработки и подходы, которыми мы руководствуемся. 
  
  Код должен быть:
  
  - Понятным, явным. Явное лучше, чем неявное. Например, не должны использоваться магические методы. 
  - Удобным для использования сейчас
  - Удобным для использования в будущем
  - Должен стремиться к соблюдению принципов [KISS](https://ru.wikipedia.org/wiki/KISS_(%D0%BF%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF)), [SOLID](https://ru.wikipedia.org/wiki/SOLID_(%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5)), [DRY](https://ru.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself), [GRASP](https://ru.wikipedia.org/wiki/GRASP)
  - Код должен обладать низкой связанностью и высокой связностью (подробно это описано в GRASP). Любая часть системы должна иметь изолированную логику и при надобности внешний интерфейс, который позволяет с этой логикой работать. Любая внутренняя часть должна иметь возможность быть измененной без какого-либо ущерба внешним системам
  - Код должен быть таким, чтобы его можно было автоматически отрефакторить в IDE (например, Find usages и Rename в WebStorm).
  - Последовательным. Код должен читаться сверху вниз. Читающий не должен держать что-то в уме, возвращаться назад и интерпретировать код иначе. Например, надо избегать обратных циклов `do {} while ();` 
  - Должен иметь минимальную [цикломатическую сложность](https://ru.wikipedia.org/wiki/%D0%A6%D0%B8%D0%BA%D0%BB%D0%BE%D0%BC%D0%B0%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B0%D1%8F_%D1%81%D0%BB%D0%BE%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D1%8C)
  
  **Общие правила**
   
   **📖 Запрещен неиспользуемый код**
   
   Если код можно убрать, и работа системы от этого не изменится, его быть не должно.
   
   Плохо:
   ```js
   if (false) {
       legacyMethodCall();
   }
   // ...
   const legacyCondition = true;
   if (legacyCondition) {
       finalizeData(data);
   }
   ```
   
   Хорошо:
   ```js
   // ...
   finalizeData(data);
   ```
   
   ***📖 Не должны напрямую использоваться функции библиотек JavaScript, если этого можно избежать***
   
   Это упростит миграцию кода на новую библиотеки JS. Часто выходят новые библиотеки или обновляются текущие, их интерфейс использования может быть изменен. Чем меньше идет завязки на библиотеку и ее версию, тем лучше.
   
   Специфичные функции всегда лучше использовать через функции-обёртки внутри проекта. Тогда в случае миграции придется исправлять одно место, а не тысячу.
   
   Как понять, можно ли использовать JS функцию или нет?
   
   - Если эта функция уже используется повсеместно в проекте, значит, её можете использовать и вы. Например, это может быть `Array.reduce`/`Array.map`. Если эти функции будут изменены в новом стандарте JS, то в любом случае придется переделать много кода и делать это будет автоматика.
   
   - Если эта функция не используется или используется только через обёртку в специализированном сервисе, то и вы использовать её можете только через обёртку (добавляется при необходимости).
   
   Плохо:
   ```js
   const arr = [1, 3, 5, 6, 2, 3, 5, 6];
   const sortedArray = arr.sort();
   ```
   
   Хорошо:
   ```js
   const arr = [1, 3, 5, 6, 2, 3, 5, 6];
   const sortedArray = arrayService.sort(arr);
   ```
   
   **Работа с переменными**
   
   ***📖 Название переменных пишутся через camelCase***
   
   ****📖 Название переменных должно соответствовать содержанию****
   
   Нельзя писать короткие названия, например `a,b,c`. Нельзя назвать переменную `day` и хранить в ней массив статистических данных за этот день.
   
   ***📖 Признак объекта добавляется к названию***
   Если это отфильтрованный по какому-то признаку массив `users`, то признак добавляется к названию. Например пользователи, которые являются администраторами, `adminUsers`.
   
   ***📖 Часто упоминаемые объекты именуются одинаково во всем проекте***
   
   Плохо:
   ```js
   const customer = new User();
   const client = new User();
   const object = new User();
   ```
   
   Хорошо:
   ```js
   const user = new User();
   ```
   
   ***📖 Переменные, отражающие свойства объекта, должны включать название объекта***
   
   Плохо:
   ```js
   const project = new Project();
   const name = project.name;
   const version = project.version;
   ```
   
   Хорошо:
   ```js
   const project = new Project();
   const projectName = project.name;
   const projectVersion = project.version;
   ```
   
   ***📖 Переменные по возможности должны называться на корректном английском***
   
   Плохо:
   ```js
   const usersStored = [];
   ```
   
   Хорошо:
   ```js
   const storedUsers = [];
   ```
   
   Исключение: сгруппированные по некому признаку поля или константы. В этом случае можно использовать префикс.
   
   ```js
   class ProjectInfo {
       STATUS_READY = 1;
       STATUS_BLOCKED = 2;
   
       billingIsPaid;
       billingPaidDate;
       billingSum;
   }
   ```
   
   ***📖 Переменные и свойства объекта должны являться существительными и называться так, чтобы они правильно читались при использовании, а не при инициализации.***
   
   Плохо:
   ```js
    const obj = {
      expireAt: '12.12.2000',
      setExpireAt: date => {},
      getExpireAt: date => {}
    }
  
   ```
   
   Хорошо:
   ```js
    const obj = {
      expirationDate: '12.12.2000',
      setExpirationDate: () => {},
      getExpirationDate: () => {}
    };
   ```
   
   ***📖 В названии переменной не должно быть указания типа***
   
   Нельзя писать `projectsArray`, надо писать просто `projects`. Это же касается и форматов (JSON и т.п.), и любой другой не относящейся к предметной области информации.
   
   Плохо:
   ```js
   const projectsList = repository.loadProjects();
   const projectsListIds = utils.extractField('id', projectsList);
   ```
   
   Хорошо:
   ```js
   const projects = repository.loadProjects();
   const projectsIds = utils.extractField('id', projects);
   ```
   
   ***📖 Нельзя изменять переменные, которые передаются в метод на вход***
    
   Исключение — если эта переменная объект.
   
   Плохо:
   ```js
   function parseText(text) {
       text = text + 'newString';
       // ...
   }
   ```
   
   Хорошо:
   ```js
   function parseText(text) {
       const preparedText = text + 'newString';
       // ...
   }
   ```
   
   ***📖 Каждая переменная должна быть объявлена на новой строке***
   
   Плохо:
   ```js
   const foo = false; const bar = true;
   ```
   
   Хорошо:
   ```js
   const foo = false;
   const bar = true;
   ```
   
   ***📖 Нельзя нескольким переменным присваивать одно и то же значение***
   
   Плохо:
   ```js
   function loadUsers(ids = []) {
       const usersIds = ids;
       // ...
   }
   ```
   
   **Логические переменные и методы**
   
   ***📖 Названия boolean методов и переменных должны содержать глагол `is`, `has` или `can`***
   
   Переменные правильно называть, описывая их содержимое, а методы — задавая вопрос. Если переменная содержит свойство объекта, следуем правилу [признак объекта добавляется к названию](#-Признак-объекта-добавляется-к-названию).
   
   Плохо:
   ```js
   const validUser = user.isValid();
   const createCampaignAccess = access.has('CREATE_CAMPAIGN'); 
   ```
   
   Хорошо:
   ```js
   const isValidUser = user.isValid();
   const canCreateCampaignAccess = access.has('CREATE_CAMPAIGN'); 
   ```
   
   Такое именование позволяет легче читать условия:
   
   ```js
   // if user is valid, then do something
   if (isValidUser) {
       // do something
   }
   
   if (canCreateCampaignAccess) {
      // do something
   }
   ```
   
   ***📖 Запрещены отрицательные логические названия***
   
   Плохо:
   ```js
   if (project.isInvalid()) {
       // ...
   }
   if (project.isNotValid()) {
       // ...
   }
   if (accessManager.isAccessDenied()) {
       // ...
   }
   ```
   
   Хорошо:
   ```js
   if (!project.isValid()) {
       // ...
   }
   if (!accessManager.isAccessAllowed()) {
       // ...
   }
   if (accessManager.canAccess()) {
       // ...
   }
   ```
   
   ***📖 Не используйте boolean переменные (флаги) как параметры функции***
   
   Флаг в качестве параметра это признак того, что функция делает больше одной вещи, нарушая [принцип единственной ответственности (Single Responsibility Principle или SRP)](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF_%D0%B5%D0%B4%D0%B8%D0%BD%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D0%B9_%D0%BE%D1%82%D0%B2%D0%B5%D1%82%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8). Избавляйтесь от них, выделяя код внтури логических блоков в отдельные ветви выполнения.
   
   Плохо:
   ```js
   function someMethod() {
       // ...
       const projectNotificationIsEnabled = notificationManager.isProjectNotificationEnabled(project);
       storeUser(user, projectNotificationIsEnabled);
   }
   
   function storeUser(user, isNotificationEnabled) {
       // ...
       if (isNotificationEnabled) {
           console.log('new user');
       }
   }
   ```
   
   Хорошо:
   ```js
   function someMethod() {
       // ...
       storeUser(user);
       if (notificationManager.isProjectNotificationEnabled(project)) {
           console.log('new user');
       }
   }
   
   function storeUser(user) {
       // ...
   }
   ```
   
   **Работа с методами**
   
   ***📖 Название метода должно начинаться с глагола и соответствовать правилам именования переменных.***
   
   Плохо:
   ```js
   function items() {
       // ...
   }
   function convertedDataObject(data = []) {
       // ...
   }
   ```
   
   Хорошо:
   ```js
   function loadItems() {
       // ...
   }
   function convertDataToObject(data = []) {
       // ...
   }
   ```
   
   ***📖 Нельзя использовать глагол get в геттерах***
   
   Например, вместо `getDate()` следует писать `date()`. Геттер — метод, работающий только с полями своего объекта.
   
   Плохо:
   ```js
   class User {
       _date;
       _customFields;
   
       getDate() {
         return this._date;
       }
   
       getCustomFields() {
         return this._customFields;
       }
   }
   ```
   
   Хорошо:
   ```js
    class User {
      _date;
      _customFields;
    
      date() {
        return this._date;
      }
    
      customFields() {
        return this._customFields;
      }
    }
   ```
   
   ***📖 Использование рекурсий допускается только в исключительном случае***
   
   Если код без рекурсии будет очень сложен для написания и понимания и при этом рекурсия гарантированно не выйдет за ограничения стека вызовов.
   
   ***📖 Параметры в методах должны следовать в следующем порядке: обязательные → часто используемые → редко используемые***
   
   Нужно соблюдать читаемость при написании вызова.
   
   Плохо:
   ```js
   function method(required, practicallyUnused = 5, often = [], lessOften = null) {}
   function filter(value, name, operator) {}
   ```
   
   Хорошо:
   ```js
   function method(required, often = [], lessOften = null, practicallyUnused = 5) {}
   function filter(name, operator, value) {}
   ```
   
   **Возврат результата работы метода**
   
   ***📖 Метод всегда должен возвращать только одну структуру данных (или `null`) или ничего не возвращать***
   
   Метод не может в разных ситуациях возвращать разные типы данных.
   
   Плохо:
   ```js
   function loadUser() {
       if (someCondition) {
           return {a:2, b:3};
       }
       return new User();
   }
   ```
   
   Хорошо:
   ```js
   function loadUser() {
       if (someCondition) {
           const user = new User();
           return user;
       }
       
       return new User();
   }
   ```
   
   ***📖 Если метод возвращает один объект (или скалярный тип), то в случае, если объект не найден, возвращается `null`***
   
   Если же метод возвращает список объектов, то в случае, когда список пуст, возвращает пустой массив. Нельзя возвращать вместо пустого списка `null`.
   
   Плохо:
   ```js
   function loadUsers() {
       if (someCondition) {
           return null;
       }
       
       return [new User()];
   }
   ```
   
   Хорошо:
   ```js
   function loadUsers() {
       if (someCondition) {
           return [];
       }
       
       return [new User()];
   }
   ```
   
   ***📖 Метод должен придерживаться следующей структуры: Проверка параметров → Получение данных → Работа → Результат***
   
   Во время проверки параметров и получения необходимых данных метод должен возвращать соответствующее пустое значение или кидать исключение. После того как метод получил все необходимые данные и приступил к работе выход из метода крайне нежелателен. Возможны редкие исключения, облегчающие понимание и читаемость кода.
   
   Плохо:
   ```js
   function someMethod() {
       const isValid = this.someCheck();
       if (isValid) {
           const tmp = 0;
           const someValue = this._getSomeValue();
           
           if (someValue > 0) {
               tmp = someValue;
           }
           
           const anotherValue = this._getAnotherValue();
           if (anotherValue > 0) {
               return tmp + anotherValue;
           } else {
               return someValue;
           }
       } else {
           throw new Error('Invalid condition');
       }
   }
   ```
   
   Хорошо:
   ```js
   function someMethod() {
       let result = 0;
        
       const isValid = this._someCheck();
       if (!isValid) {
           throw new Error('Invalid condition');
       }
     
       const someValue = this._getSomeValue();
       if (someValue > 0) {
           result += someValue;
       }
       
       const anotherValue = this._getAnotherValue();
       if (anotherValue > 0) {
           result += anotherValue;
       }
       
       return result;
   }
   ```
   
   **Работа с объектами**
   
   ***📖 Все объекты должны быть неизменяемыми (immutable), если от них не требуется обратного***

   **Комментирование кода**
   
   ***📖 В общем случае комментарии запрещены***
   
   Желание добавить комментарий — признак плохо читаемого кода. Любой участок кода, который вы хотели бы выделить или прокомментировать, надо выносить в отдельный метод.
   
   Фразу, которую вы хотели написать в комментарии, надо привести в простой вид и сделать ее названием метода.
   
   Плохо:
   ```js
   function deleteApprovedUsers() {
       // load users filter them by approval
       const users = api.loadUsers();
       const approvalUsers = users.filter(user => user.isApproved);
       
       api.removeUsers(approvalUsers);
   }
   ```
   
   Хорошо:
   ```js
   function deleteApprovedUsers() {
       const approvedUsers = this.loadApprovedUsers();
       api.remove(approvedUsers);
   }
   
   function loadApprovedUsers() {
       const users = api.loadUsers();
       return users.filter(user => user.isApproved);
   }
   ```
   
   ***📖 Готовые алгоритмы, взятые из внешнего источника, должны быть помечены ссылкой на источник***
   
   Хорошо:
   ```js
   /**
    * https://en.wikipedia.org/wiki/Quicksort
    */
   function quickSort(array = []) {
       // ...
   }
   
   /**
    * https://habrahabr.ru/post/320140/
    */
   function generateRandomMaze() {
       // ...
   }
   ```
   
   **Особенности Pull Request (PR)**
   
   ***📖 PR должен содержать как можно меньше строк кода***
   
   Любая атомарная часть кода должна выделяться в отдельную подзадачу и отдельный PR.
   
   ***📖 Нельзя смешивать перенос методов в другие классы и места и последующий рефакторинг между собой***
   
   Перенос методов в другие классы и места должны быть выделены в отдельный PR. Последующий рефакторинг после переноса тоже должен быть в отдельном PR.
   
   ***📖 В случае большого PR — ответственность за долгий просмотр несет сам разработчик, сделавший такой PR***
   
   Нормальный объем кода — 0-300 строк в зависимости от его сложности. PR заглушек и архитектуры может содержать много формального кода, который легко быстро проверить. PR же конкретного метода может содержать много сложностей даже в 10 строчках. 
   
   ***📖 Нельзя накапливать изменения в какой-то своей ветке и потом делать большой PR в master***
   
   Все что можно смержить в master без последствий (даже если это еще не готовый результат, а только заглушки или часть, но они скрыты от юзеров и никому не мешают), должен мержиться в master и PR должен создаваться в master.
   
   ***📖 В Pull Request не должно попадать кода, не относящегося к задаче***
   
   Также не должно быть забытых комментариев, бессмысленных переносов строк и прочего "строительного мусора". Каждое изменение, которое вы предлагаете сделать в master-ветке, должно так или иначе относиться к решению поставленной вам задачи.
   
   **Работа с условиями**
   
   ***📖 В условном операторе должно проверяться исключительно `boolean` значение***
   
   Плохо:
   ```js
   if (userProjects.length) {
       // ...
   }
   if (project) {
       // ...
   }
   ```
   
   Хорошо:
   ```js
   if (isResponseError) { // isResponseError = true
       // ...
   }
   if (response.isError()) { // isError method returns boolean
       // ...
   }
   if (userProjects.length > 0) {
       // ...
   }
   ```
   
   ***📖 В сравнении не boolean переменных используется строгое сравнение с приведением типа (===), автоматическое приведение и нестрогое сравнение не используются***
   
   Плохо:
   ```js
   if (project) {
       // ...
   }
   if (user.age == 100) {
       // ...
   }
   if (users.comment) {
  
   }

   ```
   
   Хорошо:
   ```js
   if (project === null) { // project is an object
       // ...
   }
   if (Number(user.age) === 100) {
       // ...
   }
   
   if (users.comment === '') {
       // ...
   }
   ```
   
   ***📖 Не надо сравнивать `boolean` с `true`/`false`***
   
   Это нарушает запрет на бесполезный код.
   
   Плохо:
   ```js
   if (bill.isPaid() == true) {
       // ...
   }
   if (bill.isPaid() !== false) {
       // ...
   }
   if (bill.isPaid() === true) {
       // ...
   }
   if (!(!bill.isPaid() === true)) {
       // ...
   }
   if (Boolean(phone.is_external) === true) {
       // ...
   }
   ```
   
   Хорошо:
   ```js
   if (bill.isPaid()) {
       // ...
   }
   ```
   ***📖 При использовании в условном выражении одновременно операторов И и ИЛИ обязательно выделять приоритет скобками***
   Обратите внимание на различие в значении двух вариантов правильного использования
   
   Плохо:
   ```js
   if (isMobile || isSizeTooBig && isAllowedToShrink) {
       // ...
   }
   ```
   
   Хорошо:
   ```js
   if ((isMobile || isSizeTooBig) && isAllowedToShrink) {
       // ...
   }
   if (isMobile || (isSizeTooBig && isAllowedToShrink)) {
       // ...
   }
   ```
   
   **Работа с тернарными операторами**
   
   ***📖 При использовании тернарных операторов действуют те же правила, что и при использовании условий***
   
   ***📖 Тернарный оператор следует использовать, если обе ветви условия предназначены для установки одной переменной одним языковым выражением***
   
   При наличии логики в ветках условия следует рассмотреть возможность вынести ее в отдельный метод.
   
   Плохо:
   ```js
   if (isExternal) {
       bill = this.loadExternalBill();
   } else {
       bill = this.loadInternalBill();
   }
   ```
   
   Хорошо:
   ```js
   bill = isExternal ? this.loadExternalBill() : this.loadInternalBill();
   ```

  **Работа с React компонентами**
  
  Основные ценности:
  
  > Любой React компонент должен быть написан таким образом, чтобы другой разработчик смог самостоятельно разобраться в логике его работы.
  
  > Код компонента должен быть самодокументируемым
  
  > Любой React компонент должен иметь понятное и простое в использовании API
  
   ***📖 В любом React компоненте необходимо прописывать подробные propTypes и defaultProps, если таковые имеются***
   
   Это необходимо для того, чтобы любой разработчик мог четко понимать с какими типами данных работает этот компонент.
   
   Плохо:
   ```js
   class MyClass extends React.Component{
     static propTypes = {
      myObj: PropTypes.obj,
      myArr: PropTypes.array 
     }
   }
   ```
      
  Хорошо:
  ```js
  class MyClass extends React.Component {
    static propTypes = {
      myObj: PropTypes.shape({
        prop1: PropTypes.string,
        prop2: PropTypes.Number.isRequired,
        ...
      }),
      myArr: PropTypes.arrayOf(
        PropTypes.shape({
          prop1: PropTypes.string,
          prop2: PropTypes.number,
          prop3: PropTypes.shape({
            nestedProp1: PropTypes.string.isRequired
          }),
         ...
        })
      )
    }
    
    static defaultProps = {
      myObj: {
        prop1: 'Value1',
        prop2: 999
      }
    }
  }
  ```        
  
  ***📖 Нельзя хранить логику в методе render***  
  
  Плохо:
  ```js
     class MyClass extends React.Component {
  
       render() {
         return (
           <SomeComponent onClick={(data) => {
             const { onChange } = this.props;
             const newData = data.map({key, id} => key);
             this.setState({ data: newData }, () => {
               onChange(newData);
             });
           }}/>
         );
       }
       
     }
  ```
  Хорошо:
  ```js
       class MyClass extends React.Component {
  
         handleSomeComponentChange = data => {
           const { onChange } = this.props;
           const newData = data.map(({ key }) => key);
           this.setState({ data: newData }, () => {
             onChange(newData);
           });
         }
      
         render() {
           return (
             <SomeComponent onClick={this.handleSomeComponentClick}/>
           );
         }
       }
  ```        
  
  
  
  

   
