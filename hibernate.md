HIBERNATE
## 1. What is the ORM design pattern? How does it work?
   ORM или объектно-реляционное отображение - это система, которая реализует ответственность за отображение объекта в реляционную модель. Это означает, что он отвечает за хранение данных объектной модели в реляционной модели и последующее считывание данных из реляционной модели в объектную модель.  
   ORM состоит из:
   API, который реализует базовые операции (СОЗДАНИЕ, ЧТЕНИЕ, ИЗМЕНЕНИЕ, УДАЛЕНИЕ) объектов-моделей.
   Средства настройки метаданных связывания
   Технику взаимодействия с транзакциями, которая позволяет реализовать такие функции, как dirty checking, lazy association fetching и т.д.
## 2. Advantages of ORM.
   Преимущества ORM в сравнение с JDBC?
   Позволяет бизнес методам обращаться не к БД, а к Java-классам
   Ускоряет разработку приложения
   Основан на JDBC
   Отделяет SQL-запросы от ОО модели
   Позволяет не думать о реализации БД
   Сущности основаны на бизнес-задачах, а не на стуктуре БД
   Управление транзакциями
## 3. Hibernate Framework overview.
   Hibernate – это ORM фреймворк для Java с открытым исходным кодом. Эта технология является крайне мощной и имеет высокие показатели производительности.
   Hibernate создаёт связь между таблицами в базе данных (далее – БД) и Java-классами и наоборот. Это избавляет разработчиков от огромного количества лишней, рутинной работы, в которой крайне легко допустить ошибку и крайне трудно потом её найти.
   Преимущества Hibernate:
   Обеспечивает простой API для записи и получения Java-объектов в/из БД.
   Минимизирует доступ к БД, используя стратегии fetching.
   Не требует сервера приложения.
   Позволяет нам не работать с типами данных языка SQL, а иметь дело с привычными нам типами данных Java.
   Заботится о создании связей между Java-классами и таблицами БД с помощью XML-файлов не внося изменения в программный код.
   Если нам необходимо изменить БД, то достаточно лишь внести изменения в XML-файлы.
## 4. Hibernate and ORM.
## 5. JPA overview. Hibernate and JPA.
   JPA (Java Persistence API) это спецификация Java EE и Java SE, описывающая систему управления сохранением java объектов в таблицы реляционных баз данных в удобном виде. Сама Java не содержит реализации JPA, однако существует много реализаций данной спецификации от разных компаний. Это не единственный способ сохранения java объектов в базы данных (ORM систем), но один из самых популярных в Java мире.
   Hibernate одна из самых популярных открытых реализаций последней версии спецификации (JPA 2.1). Даже скорее самая популярная, почти стандарт де-факто. То есть JPA только описывает правила и API, а Hibernate реализует эти описания, впрочем у Hibernate (как и у многих других реализаций JPA) есть дополнительные возможности, не описанные в JPA (и не переносимые на другие реализации JPA)
## 6. Hibernate vs JDBC: Advantages and disadvantages of using.
   Hibernate – это Framework работы ORM
   JDBC – подключение к базе данных.
   Преимущества Hibernate перед JDBC:
   В Hibernate есть транслятор исключений, который преобразует проверенные исключения JDBC в непроверенные исключения Hibernate. Таким образом, все исключения в Hibernate - это непроверенные исключения, и из-за этого нет необходимости явно обрабатывать исключения.
   Hibernate поддерживает наследование и полиморфизм.
   С помощью Hibernate можно управлять данными, хранящимися в нескольких таблицах, применяя отношения (ассоциации)
   Hibernate имеет собственный язык запросов, называемый Hibernate Query Language (HQL). Благодаря этому Hibernate HQL стал независимым от базы данных.
   Hibernate поддерживает такие отношения, как «один-к-одному», «один-ко-многим», «многие-к-одному», «многие-ко-многим».
   Hibernate имеет механизм кэширования. Использование этого количества обращений к базе данных будет уменьшено. Поэтому производительность приложения будет увеличиваться.
   Hibernate поддерживает множество баз данных.
   Hibernate - это легкий фреймворк, потому что hibernate использует классы POJO для передачи данных между приложением и базой данных.
   Hibernate имеет функцию управления версиями и отметки времени, благодаря чему можно узнать, сколько раз данные были изменены.
   Hibernate также поддерживает аннотации вместе с XML.
   Hibernate поддерживает отложенную загрузку.
   Hibernate легко освоить, он удобен для разработчиков.
   Архитектура многоуровневая, чтобы изолировать от необходимости знать базовые API.
   Hibernate поддерживает пул соединений с базой данных.
   Hibernate поддерживает параллелизм.
   Используя Hibernate, его легко поддерживать, и он увеличивает производительность
   Недостатки Hibernate по сравнению с JDBC:
   Hibernate работает медленнее по сравнению с JDBC из-за генерации множества SQL-запросов во время выполнения.
   Тяжеловесный для небольших проектов
## 7. Hibernate important interfaces.
   Элементы Hibernate:
   Transaction – этот объект представляет собой рабочую единицу работы с БД. В Hibernate транзакции обрабатываются менеджером транзакций.
   SessionFactory – самый важный и самый тяжелый объект (обычно создаётся в единственном экземпляре, при запуске приложения). Нам необходима как минимум одна SessionFactory для каждой БД, каждый из которых конфигурируется отдельным конфигурационным файлом.
   Session – сессия используется для получения физического соединения с БД. Обычно, сессия создаётся при необходимости, а после этого закрывается. Это связано с тем, что эти объекты крайне легковесны.
   Query – этот объект использует HQL или SQL для чтения/записи данных из/в БД. Экземпляр запроса используется для связывания параметров запроса, ограничения количества результатов, которые будут возвращены и для выполнения запроса.
   Configuration – этот объект используется для создания объекта SessionFactory и конфигурирует сам Hibernate с помощью конфигурационного XML-файла, который объясняет, как обрабатывать объект Session.
   Criteria – используется для создания и выполнения объекто-ориентированных запроса дял получения объектов.
## 8. Hibernate configuration file.
   Файл конфигурации hibernate.cfg.xml содержит информацию о базе данных (драйвер, пул подключений, диалект) и параметрах подключения к серверу БД (url, login, password). В качестве параметров подключения можно использовать как JDBC, так и JNDI. В файле конфигурации также определяются дополнительные параметры, которые будут использованы при работе с сервером БД, Так, здесь необходимо определить маппинги сущностей/классов.
   Свойства:
   hibernate.dialect – Указывает HIebrnate диалект БД. Hibernate, в своб очередь, генерирует необходимые SQL-запросы (например, org.hibernate.dialect.MySQLDialect, если мы используем MySQL).
   hibernate.connection-driver_class – Указывает класс JDBC драйвера.
   hibernate.connection.url – Указывает URL (ссылку) необходимой нам БД (например, jdbc:mysql://localhost:3306/database).
   hibernate.connection.username – Указывает имя пользователя БД (например, root).
   hibernate.connection.password – Укащывает пароль к БД (например, password).
   hibernate.connection.pool_size – Ограничивает количество соединений, которые находятся в пуле соединений Hibernate.
   hibernate.connection.autocommit – Указывает режим autocommit для JDBC-соединения.
## 9. Hibernate mapping file.
   Файл отображения (mapping file) используется для связи entity бинов с таблицами базы данных. Содержимое файла имеет формат XML. Файл mapping можно использовать вместо аннотаций JPA. Особенно он становится необходимым при использовании сторонних библиотек.
   Свойства:
   <hibernate-mapping> - Это ключевой тег, который должен быть в каждом XML – фалйе для связывания (mapping). Внутри этого тега конфигурируются связи.
   <class> - Тег <class> используется для того, чтоы указать связь между POJO – классом и таблицей в БД. Имя класса указывается с помощью свойства name, имя таблицы в БД – с помощью свойства table.
<meta>- Опциональный (необязательный) тег, внутри которого можно добавить описание класса.
<id> - Тег <id > связывает уникальный идентификатор ID в POJO – классе и первичный ключ (primary key) в таблице БД. Свойство name соединяет поле класса со свойством column, которое указывает нам колонку в таблице БД. Свойство type определяет тип связывания (mapping) и используется для конфертации типа данных Java в тип данных SQL.
<generator> - Этот тег внутри тега <id> используется для того, что генерировать первичные ключи автоматически. Если указать это свойство native, то Hibernate сам выберет алгоритм (identity, hilo, sequence) в зависимости от возможностей БД.
<property> - Этот тег используется для того, чтобы связать (map) конкретное поле POJO – класса с конкретной колонкой в таблице БД. Свойство name указывает поле в классе, в то время как свойство column указывает на колонку в таблице БД. Свойство type указывает тип связывания (mapping) и конвертирует тип данных Java в тип данных SQL.
10.  SessionFactory and Session in Hibernate.
Сессия используется для получения физического соединения с базой данных.
С помощью сессии объекты  создаются, читаются, редактируются и удаляются.
Сессии не являются потоко-защищенными и не должны быть открыты в течение длительного времени.
Экземпляр класса может находиться в одном из трех состояний:
Transient – Это новый экземпляр класса, который не привязан к сессии и еще не представлен в БД. Он не имеет значения, по которому может быть идентифицирован.
Persistent – Можно создать переходный экземпляр класса, связав его с сессией.
Detached – После того, как сессия закрыта, экземпляр класса становится отдельным, независимым экземпляром класса.




SessionFactory


Экземпляр SessionFactory создается методом buildSessionFactory   (ServiceRegistry) объекта org.hibernate.Configuration и предназначен для получения объекта Session. Инициализируется SessionFactory один раз. Внутреннее состояние SessionFactory неизменно (immutable), т.е. он является потокобезопасным. Internal state (внутреннее состояние) включает в себя все метаданные об Object Relational Mapping, определяемые при создании SessionFactory.

SessionFactory также предоставляет методы для получения метаданных класса и статистики, типа данных о втором уровне кэша, выполняемых запросах и т.д.
Session

Однопоточный объект, устанавливающий связь   между объектами/сущностями приложения и базой данных. Сессия создается при необходимости работы с БД и ее необходимо закрыть сразу же после использования. Экземпляр Session является интерфейсом между кодом в java приложении и hibernate framework, предоставляя методы для операций CRUD.

Transaction
Однопоточный объект, используемый для атомарных операций. Это абстракция приложения от основных JDBC или JTA транзакций. org.hibernate.Session может занимать несколько org.hibernate.Transaction в определенных случаях.

## 11. Hibernate caching. Levels of cache.
Hibernate предлагает два уровня кэширования:
    Кэш первого уровня - это кеш сеанса. Объекты кэшируются в текущем сеансе, и они живы только до закрытия сеанса.
    Кэш второго уровня существует, пока жива фабрика сеансов. Имейте в виду, что в случае Hibernate кеш второго уровня не является деревом объектов; экземпляры объекта не кэшируются, вместо этого хранятся значения атрибутов.
## 12. Session merge vs call.
Метод Hibernate merge объекта сессии может быть использован для обновления существующих значений. Необходимо помнить, что данный метод создает и возвращает копию из переданного объекта сущности. Возвращаемый объект является частью контекста персистентности с отслеживанием любых изменений, а переданный объект не отслеживается.
## 13.  Save vs saveOrUpdate vs persist.
Метод save используется для сохранения сущности в базе данных. Этот метод возвращает сгенерированный идентификатор. Возникающие проблемы с использованием save связаны с тем, что метод может быть вызван без транзакции. А следовательно если имеется отображение нескольких связанных объектов, то только первичный объект будет сохранен, т.е. можно получить несогласованные данные.
     Метод hibernate persist аналогичен save, но выполняется с транзакцией. Метод persist не возвращает сгенерированный идентификатор сразу.
     Метод saveOrUpdate используется для вставки или обновления сущности. Если объект уже присутствуют в базе данных, то будет выполнен запрос обновления. Метод saveOrUpdate можно
     применять без транзакции, но это может привести к аналогичным проблемам, как и в случае с методом save.
## 14. Joins implementation in Hibernate.
Есть разные способы реализовать соединения в Hibernate.
    Используя ассоциации, такие как "один к одному", "один ко многим"
    @OneToOne
    (mappedBy="employee")
    @Cascade
    (value=org.hibernate.annotations.CascadeType.ALL)
    Используя JOIN в запросе HQL, и используя собственный запрос sql с ключевым словом join.
## 15. Lazy loading in Hibernate.
Ленивая загрузка – это механизм, предоставляемый Hibernate для повышения эффективности выполнения программ, а именно создается только тогда, когда данные объекта фактически используются.
    Преимущества:
    Время начальной загрузки намного меньше, чем при другом подходе
    Меньшее потребление памяти, чем при другом подходе
    Недостатки:
    Отложенная инициализация может повлиять на производительность в нежелательные моменты.
    В некоторых случаях вам нужно обрабатывать лениво инициализированные объекты с особой осторожностью, иначе вы можете получить исключение.
## 16. HQL overview.
Hibernate Query Language (HQL) - это объектно-ориентированный язык запросов, похожий на SQL, но вместо работы с таблицами и столбцами HQL работает с постоянными объектами и их свойствами. Запросы HQL переводятся Hibernate в обычные запросы SQL, которые, в свою очередь, выполняют действия с базой данных.
    Хотя вы можно использовать операторы SQL напрямую с Hibernate, используя собственный SQL, рекомендуется использовать HQL, когда это возможно, чтобы избежать проблем с переносимостью базы данных и воспользоваться преимуществами стратегий генерации и кэширования SQL Hibernate.
    Примеры:
1. Query query = session.createQuery("FROM Developer");
2. Query query = session.createQuery("INSERT INTO Developer (firstName, lastName, specialty, experience)");
3. Query query = session.createQuery(UPDATE Developer SET experience =: experience WHERE id =: developerId);
   query.setParameter("experience", 3);
4. Query query = session.createQuery("DELETE FROM Developer WHERE id = :developerId");
   query.setParameter("developerId", 1);
5. Query query = session.createQuery("SELECT D.lastName FROM Developer D");
6. Query query = session.createQuery("FROM Developer D WHERE experience > 3 ORDER BY D.experience DESC");
7. Query query = session.createQuery("FROM Developer D WHERE D.id = 1");
## 17. Query cache in Hibernate.
 Hibernate реализует область кэша для запросов ResultSet, который тесно взаимодействует с кэшем второго уровня Hibernate. Для подключения этой дополнительной функции необходимо определить истинное значение свойства hibernate.cache.use_query_cache в файле конфигурации hibernate.cfg.xml и в коде при обращении к БД использовать метод setCacheable(true). Кэшированные запросы полезны только при их частом исполнении с повторяющимися параметрами.
    Определение свойства в файле конфигурации Hibernate :
    <property name="hibernate.cache.use_query_cache">true</property>
    Формирование запроса с использованием метода setCacheable (true) :
    Query query = session.createQuery("from Employee");
    query.setCacheable(true);
    query.setCacheRegion("ALL_EMP");
## 18. Different types of cascading.
При наличии зависимостей (связей) между сущностями необходимо определить влияние различных операций одной сущности на связанные. Это можно реализовать с помощью аннотации каскадных связей @Cascade.
    Пример использования @Cascade :
    import org.hibernate.annotations.Cascade;
    @Entity
    @Table(name = "EMPLOYEE")
    public class Employee {
    @OneToOne (mappedBy="employee")
    @Cascade (value=org.hibernate.annotations.CascadeType.ALL)
    private Address address;
    }
Помните, что имеются некоторые различия между enum CascadeType в Hibernate и в JPA. Поэтому обращайте внимание на импортируемый пакет при использовании аннотации и константы типа. Наиболее часто используемые CascadeType перечисления описаны ниже:
    None: без каскадирования, т.е. никакая операция для родителя не будет иметь эффекта для наследника;
    ALL: все операции родителя будут отражены на наследнике (save, delete, update, evict, lock, replicate, merge, persist);
    SAVE_UPDATE: операции save и update, доступно только для hibernate;
    DELETE: в Hibernate передается действие native DELETE;
    DETATCH, MERGE, PERSIST, REFRESH, REMOVE – для простых операций;
    LOCK: передает в Hibernate native LOCK действие;
    REPLICATE: передает в Hibernate native REPLICATE действие.