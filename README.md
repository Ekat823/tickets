#### Билеты на событие  

1. Добавляем требуемые поля в таблицу, в итоге она выглядит примерно так  

`CREATE TABLE orders (`  
    `id INT(11) NOT NULL,`  
    `event_id INT(11) NOT NULL,`  
    `event_date DATETIME NOT NULL,`  
    `ticket_adult_price DOUBLE NOT NULL,`  
    `ticket_adult_quantity INT(11) NOT NULL,`  
    `ticket_kid_price DOUBLE NOT NULL,`  
    `ticket_kid_quantity INT(11) NOT NULL,`  
    `ticket_group_price DOUBLE NOT NULL,`  
    `ticket_group_quantity INT(11) NOT NULL,`  
    `ticket_concession_price DOUBLE NOT NULL,`  
    `ticket_concession_quantity INT(11) NOT NULL,`  
    `barcode VARCHAR(50) NOT NULL,`  
    `equal_price DOUBLE NOT NULL,`  
    `created DOUBLE NOT NULL`  
`)`  

2. Возможно добавить возможность добавлять множество баркодов, заменив столбец barcode на barcodes с типом JSON  

`CREATE TABLE orders (`  
    `id INT(11) NOT NULL,`  
    `event_id INT(11) NOT NULL,`  
    `event_date DATETIME NOT NULL,`  
    `ticket_adult_price DOUBLE NOT NULL,`  
    `ticket_adult_quantity INT(11) NOT NULL,`  
    `ticket_kid_price DOUBLE NOT NULL,`  
    `ticket_kid_quantity INT(11) NOT NULL,`  
    `ticket_group_price DOUBLE NOT NULL,`  
    `ticket_group_quantity INT(11) NOT NULL,`  
    `ticket_concession_price DOUBLE NOT NULL,`  
    `ticket_concession_quantity INT(11) NOT NULL,`  
    `barcodes JSON NOT NULL,`  
    `equal_price DOUBLE NOT NULL,`  
    `created DOUBLE NOT NULL`  
`)`  

PS но все это не очень хорошие решения, в идеале нужно разделить таблицу на две. Тогда мы не нарушим нормализацию и сможем спокойно добавлять новые типы билетов без изменения таблиц.  

`CREATE TABLE orders (`  
    `id INT(11) NOT NULL,`  
    `event_id INT(11) NOT NULL,`  
    `event_date DATETIME NOT NULL,`  
    `equal_price DOUBLE NOT NULL`  
`)`  
    
`CREATE TABLE tickets (`  
    `id INT(11) NOT NULL,`  
    `order_id INT(11) NOT NULL,`  
    `price DOUBLE NOT NULL,`  
    `type ENUM('KID', 'GROUP', 'ADULT', 'CONCESSION') NOT NULL,`  
    `barcode VARCHAR(50) NOT NULL,`  
    `created DOUBLE NOT NULL`  
`)`
