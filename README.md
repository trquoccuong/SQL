# Báo cáo Code Camp 
----
Hãy thiết kế CSDL quan hệ trên Postgresql để mô hình hoá đủ các thông tin cần thiết để xây dựng web site, web service cung cấp thông tin dạng REST cho ứng dụng di động hiển thị:

1. Danh mục phân loại chủng loại hàng chung: [Quần áo – thời trang, Đồ chơi, Thực phẩm – đồ uống, Đồ gia dụng, Điện tử gia dụng, Di động – tablet, Máy tính – linh kiện – mạng]
2. Danh mục phân loại chủng loại hàng chi tiết: [Quần áo – thời trang: Nam, Nữ, Trẻ con], [Đồ chơi: bé trai, gái, thiếu nhi], [Thực phẩm – đồ uống: ….]…3. 
3. Do có nhiều mặt hàng cùng một loại, có nhiều tính chất chung nhau như:
Tivi các hãng sẽ có thuộc tính: [công nghệ: LED, Plasma, OLED], [màn hình: phẳng, cong], [smart: có kết nối Internet, không], [cổng giao tiếp: HDMI, USB, DNA, Bluetooth, Ethernet, Wifi] Xe máy sẽ có thuộc tính: [loại động cơ: 4 thì, 2 thì], [chuyển động: ga, số, côn tay], [dung tích: xy lanh], [màu sơn: …],….
Tất cả các mặt hàng đều có một số thuộc tính chung: Tên, mã SKU (mã để quản lý trong kho: Stock Keeping Unit, phải là duy nhất để gán mã vạch), mô tả chi tiết, nhà sản xuất, công ty phân phối, ngày sản xuất, thời gian bảo hành, hạn sử dụng, giá gốc nhập, giá bán hiện tại, bảo hành ~ hạn sử dụng.
Cần thiết kế hệ thống bảng để lưu được thông tin chung của mặt hàng và các thông tin đặc thù từng loại mặt hàng.
Các hàng cùng loại có thể so sánh được với nhau. Ví dụ khách hàng muốn so sánh xe Airblade 2014 với Exciter 150.
Cùng loại mặt hàng rõ ràng, nhưng khác một tính chất như màu sắc thì khác giá tiền. Lúc này phải tách ra thành các mã SKU độc lập. Ví dụ iPhone 6 có dung lượng khác nhau: 16G, 32G, 64G. Hoặc Exciter 150 có các màu sơn, tem khác nhau…

4. Nhà sản xuất (khác với nhà phân phối): Honda, Yamaha, Nike, Adidas, Apple, Microsoft, Sony, LG, Samsung….
Nên thiết kế một bảng riêng.
Ở mỗi phân loại chủng loại hàng chung, thường có danh mục các hãng sản xuất phù hợp. Ví dụ: mục quần áo – thời trang nên có Nike, Adidas, Northface… nhưng có thể không có Apple, Microsoft, Sony, LG, Samsung.

5. Ứng dụng có một text box để search. Trong scope của code camp này, giả sử người dùng chỉ tìm kiếm theo tên sản phẩm. Thực tế người dùng sẽ gõ từ khoá tìm kiếm phức tạp dị hơn nhiều. Do đó không thể xài SQL query để truy vấn được đâu.

### Một số lưu ý
----
1. Không phải thuộc tính nào (column) cũng phải có. Sẽ có nhiều thuộc tính là null.
2. Phải thiết kế hệ thống bảng – quan hệ đủ mềm dẻo để việc bảo trì, chỉnh sửa cấu trúc bảng là thấp nhất. Trong Postgresql 9.4 có kiểu dữ liệu JSONB giúp record có thể lưu động các loại thông tin không cần tuân thủ cấu trúc cột (column) cổ điển.
3. Do đề tài codecamp phức tạp, nên hai học viên sẽ cùng làm một bài. Techmaster sẽ cử một lập trình CSDL để trả lời các câu hỏi của các bạn qua chat.
4. Tham khảo tuyển tập các loại Database schema cho nhiều ngành ở đây [http://www.databaseanswers.org/data_models/](http://www.databaseanswers.org/data_models/)
5. Nên bắt đầu làm càng sớm tốt. Làm trước 1-2 ngày sẽ không kịp đâu.
6. Lịch code camp ngày 25/1/2015 tại số 14 ngõ 4, Nguyễn Đình Chiểu. Thực hành ở phòng lab tầng 1 và tầng 4. Đủ chỗ cho anh em.

### Gợi ý các bước làm
-----
1. Thu thập tập dữ liệu mẫu từ các web site thương mại điện tử nổi tiếng để học hỏi họ tổ chức thông tin như thế nào?
2. Vẽ khối lương các bảng đừng quan tâm các trường (cột) chi tiết vội. Chỉ cần xác định được khoá chính (`primary key`) là ok rồi.
3. Hình dung quan hệ phù hợp giữa các bảng: 1-1, kế thừa, một – nhiều, nhiều – nhiều.
4. Cùng bàn bạc với đồng đội sẽ có chỗ nào chưa ổn.
5. Tạo bảng trên Postgresql viết ra một file schema.sql để còn nộp bài. Mỗi lần sửa thì sửa trên schema.sql sau đó lưu lại. Nhớ DROP TABLE trước CREATE TABLE
6. Tạo dữ liệu mẫu, viết vào một file data.sql. Nên tạo nhiều record đa dạng để sớm phát hiện sai sót, bất cập trong thiết kể bảng. Nhớ nguyên tắc Fail Fast khi làm sản phẩm không các men.
7. Đặt nhiều câu hỏi dạng : What – If, nếu – thì để xem cấu trúc CSDL có bền không. Chỉnh lại schema.sql và data.sql cho đến khi các dữ liệu – quan hệ phù hợp.
8. Viết báo cáo bằng MkDocs


### Mô tả phương pháp xử lý chung
----
EAV hay là thiết kế cho mỗi chủng loại sản phẩm một bảng riêng hay cho thuộc tính đặc thù vào trường jsonb
	
    EAV là 1 kiểu khái niệm liên quan đến chuẩn hóa cơ sở dữ liệu. Về mặt khái niệm bạn có thể hiểu nó như sau:
       1. Theo cách tổ chức cơ sở dữ liệu đơn giản trong 1 table duy nhất cho các products theo kiểu table gồm các columns như product_id, và các product attributes, mỗi product sẽ có giá trị các attribute được lưu trong 1 row, nếu các products có thêm attributes thì phải sửa lại schema của database, thêm columns cho table.
       2. Theo cách tổ chức của mô hình EAV sẽ có ít nhất 2 tables: e.g. table 1 để định nghĩa attribute (e.g. gồm các columns như attribute_id, attribute_name, attribute_type...) và table 2 để lưu giá trị của các attribute cho từng product entity (e.g. gồm các columns như entity_id, attribute_id, attribute_value...). Khi đó giá trị các attribute của 1 entity sẽ được lưu trên nhiều row thay vì 1 row trong mô hình trên, và khi thêm 1 attribute mới, thay vì phải thêm column tức là phải thay đổi schema của database, thì chỉ cần thêm 1 row định nghĩa cho attribute mới trong table 1 và thêm các row trong table 2 chứa các giá trị của attribute mới của từng entity. 


### Các bảng quan hệ
----

![Data](/img/data.png)


### Mô tả cơ sở dữ liệu 
-----

### Sử dụng SQL generete 

```
CREATE TABLE Product_indetify (sku  SERIAL NOT NULL, price int4, instock int4, PRIMARY KEY (sku));

CREATE TABLE Catagories (idCatagory  SERIAL NOT NULL, name varchar(100), CatagoriesidCatagory int4 NOT NULL, PRIMARY KEY (idCatagory));

CREATE TABLE Detail_product (Productidproduct int4 NOT NULL, Attribute_valuestringAttributeidatrribute int4, Attribute_valuestringvaluestringidvalue int4, Product_indetifysku int4 NOT NULL);

CREATE TABLE Attribute_valuestring (Attributeidatrribute int4 NOT NULL, valuestringidvalue int4 NOT NULL, PRIMARY KEY (Attributeidatrribute, valuestringidvalue));

CREATE TABLE Product_Attribute (Productidproduct int4 NOT NULL, Attributeidatrribute int4 NOT NULL, PRIMARY KEY (Productidproduct, Attributeidatrribute));

CREATE TABLE Product_valuestring (Productidproduct int4 NOT NULL, valuestringidvalue int4 NOT NULL, PRIMARY KEY (Productidproduct, valuestringidvalue));

CREATE TABLE valuestring (idvalue  SERIAL NOT NULL, valueString varchar(100), valuestringidvalue int4 NOT NULL, PRIMARY KEY (idvalue));

CREATE TABLE Attribute (idatrribute  SERIAL NOT NULL, atribute_name varchar(100), Attributeidatrribute int4 NOT NULL, PRIMARY KEY (idatrribute));

CREATE TABLE Product (idproduct  SERIAL NOT NULL, name varchar(100), CatagoriesidCatagory int4 NOT NULL, PRIMARY KEY (idproduct));

ALTER TABLE valuestring ADD CONSTRAINT FKvaluestrin994189 FOREIGN KEY (valuestringidvalue) REFERENCES valuestring (idvalue);

ALTER TABLE Catagories ADD CONSTRAINT FKCatagories892759 FOREIGN KEY (CatagoriesidCatagory) REFERENCES Catagories (idCatagory);

ALTER TABLE Attribute ADD CONSTRAINT FKAttribute885698 FOREIGN KEY (Attributeidatrribute) REFERENCES Attribute (idatrribute);

ALTER TABLE Product ADD CONSTRAINT FKProduct864776 FOREIGN KEY (CatagoriesidCatagory) REFERENCES Catagories (idCatagory);

ALTER TABLE Detail_product ADD CONSTRAINT FKDetail_pro606548 FOREIGN KEY (Attribute_valuestringAttributeidatrribute, Attribute_valuestringvaluestringidvalue) REFERENCES Attribute_valuestring (Attributeidatrribute, valuestringidvalue);

ALTER TABLE Detail_product ADD CONSTRAINT FKDetail_pro587398 FOREIGN KEY (Productidproduct) REFERENCES Product (idproduct);

ALTER TABLE Attribute_valuestring ADD CONSTRAINT FKAttribute_882171 FOREIGN KEY (valuestringidvalue) REFERENCES valuestring (idvalue);

ALTER TABLE Attribute_valuestring ADD CONSTRAINT FKAttribute_235125 FOREIGN KEY (Attributeidatrribute) REFERENCES Attribute (idatrribute);

ALTER TABLE Product_Attribute ADD CONSTRAINT FKProduct_At28042 FOREIGN KEY (Productidproduct) REFERENCES Product (idproduct);

ALTER TABLE Product_Attribute ADD CONSTRAINT FKProduct_At428733 FOREIGN KEY (Attributeidatrribute) REFERENCES Attribute (idatrribute);

ALTER TABLE Product_valuestring ADD CONSTRAINT FKProduct_va501627 FOREIGN KEY (valuestringidvalue) REFERENCES valuestring (idvalue);

ALTER TABLE Product_valuestring ADD CONSTRAINT FKProduct_va366141 FOREIGN KEY (Productidproduct) REFERENCES Product (idproduct);

ALTER TABLE Detail_product ADD CONSTRAINT FKDetail_pro89586 FOREIGN KEY (Product_indetifysku) REFERENCES Product_indetify (sku);

```

### Nhập liệu 
----

```
Vì khối dữ liệu nhập vào để test khá lớn nên code bên dưới chỉ mô phỏng câu lệnh nhập liệu 
```

#### Nhập dữ liệu bảng "catagories"

````
INSERT INTO catagories(
            idcatagory, name, catagoriesidcatagory)
    VALUES 
        (1, 'Cellphone and Tablet',1),
        (2, 'Electronics',2),
         ....... ;
        
````

#### Nhập liệu bảng "product"

````
INSERT INTO product(
            idproduct, name, catagoriesidcatagory)
    VALUES 
        (1, 'Galaxy S5', 5),
        (2, 'Iphone 6', 5),
          ....... ;
        
````
#### Nhập liệu bảng "attribute"

````
INSERT INTO attribute(
            idatrribute, atribute_name, attributeidatrribute)
    VALUES 
        (1,'network',1),
        (2,'body',2),
          ....... ;
                
````

#### Nhập liệu bảng "valuestring"

````
INSERT INTO valuestring(
            idvalue, valuestring, valuestringidvalue)
    VALUES 
        (1, 'GSM / HSPA / LTE', 1),
        (2, 'GSM 850 / 900 / 1800 / 1900', 2),
          .......   ;
        
````

#### Nhập liệu bảng "product_attribute"

````
INSERT INTO product_attribute(
            productidproduct, attributeidatrribute)
    VALUES 
        (3, 7),
        (3, 8),
        .... ;
        
````

### Một số bước truy suất bằng lệnh "Select"
----

#### Lấy ra tên sản phẩm theo mã SKU 

````
SELECT   Product_indetify.sku as sku, product.name as name 
   FROM  Product,Product_indetify,Detail_product
   WHERE Detail_product.Product_indetifysku = Product_indetify.sku AND
   Product.idproduct = Detail_product.Productidproduct
   GROUP BY name,sku;

````
----
![sosanh](/img/sku-name.png)	

#### Lấy ra tên sản phẩm và thuộc tính tương ứng của nó qua mã SKU 

````
SELECT Product_indetify.sku as sku, product.name as name , Attribute.atribute_name as atr , valueString.valueString as vs  FROM Product,Product_indetify,Detail_product , valuestring ,Attribute
WHERE Detail_product.Product_indetifysku = Product_indetify.sku AND Product_indetify.sku = 45135 AND
Product.idproduct = Detail_product.Productidproduct AND Detail_product.Attribute_valuestringAttributeidatrribute = Attribute.idatrribute AND Detail_product.Attribute_valuestringvaluestringidvalue = valuestring.idvalue 
GROUP BY name,sku , vs , atr;

````
----
![ma-ten](/img/name-thuoc-tinh.png)

#### So sánh hai sản phẩm theo tên 

````
SELECT T1.atr, T1.iphone6,T2.galaxys5
FROM 
(SELECT Attribute.atribute_name as atr , valueString.valueString as iphone6 FROM Product,Product_indetify,Detail_product , valuestring ,Attribute
WHERE Detail_product.Product_indetifysku = Product_indetify.sku AND Product_indetify.sku = 45135  AND
Product.idproduct = Detail_product.Productidproduct AND Detail_product.Attribute_valuestringAttributeidatrribute = Attribute.idatrribute AND Detail_product.Attribute_valuestringvaluestringidvalue = valuestring.idvalue 
GROUP BY  atr,iphone6) T1

INNER JOIN

(SELECT  valueString.valueString as galaxys5 , Attribute.atribute_name as atr FROM Product,Product_indetify,Detail_product , valuestring ,Attribute
WHERE Detail_product.Product_indetifysku = Product_indetify.sku AND Product_indetify.sku = 33324  AND
Product.idproduct = Detail_product.Productidproduct AND Detail_product.Attribute_valuestringAttributeidatrribute = Attribute.idatrribute AND Detail_product.Attribute_valuestringvaluestringidvalue = valuestring.idvalue 
GROUP BY  atr,galaxys5) T2
ON 
	T1.atr = T2.atr;


```` 
-----
![sosanh](/img/so-sanh.png)	



### Người Làm !
  
   * Nhóm Cường - Phong lớp IOS 27 [Techmatter](http://techmaster.vn/)

