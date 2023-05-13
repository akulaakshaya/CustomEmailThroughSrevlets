# CustomEmailThroughSrevlets
CREATE TABLE contacts (
    serial_no SERIAL,
    name VARCHAR(255),
    mail_id VARCHAR(255) PRIMARY KEY,
    date_of_birth DATE,
	ph_no numeric(10,0)
);
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Akshaya','akshayavarma39@gmail.com','03-07-2002',9603442969);
select * from contacts;
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Varma','varmaakula506@gmail.com','04-07-1972',9247139775);
insert into contacts(name,mail_id,date_of_birth,ph_no) values('Amarthya','amarthyavarmaakula@gmail.com','21-09-1999',9848422148);
