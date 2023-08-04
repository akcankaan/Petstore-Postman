 #### 👨🏻‍💻 Pet ekle (petName=Mia) 
 ***
<details>
  <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>
 
   ```javascript
pm.test("Gövde eşleme dizesi", function () {
    pm.expect(pm.response.text()).to.include("Mia");
});

pm.test("Yanıt durum kodu 200'dür", function () {
  pm.response.to.have.status(200);
});

pm.test("Kimlik alanının negatif olmayan bir tam sayı olduğunu doğrulayın", function () {
  const responseData = pm.response.json();
  
  pm.expect(responseData).to.be.an('object');
  pm.expect(responseData.id).to.be.a('number').and.to.satisfy((id) => id >= 0, "id should be a non-negative integer");
});

pm.test("Ad alanının boş olmayan bir dize olduğunu doğrulayın", function () {
    const responseData = pm.response.json();
    
    pm.expect(responseData).to.be.an('object');
    pm.expect(responseData.name).to.be.a('string').and.to.have.lengthOf.at.least(1, "Value should not be empty");
});

pm.test("photoUrls dizisinin ve en az bir öğenin varlığını doğrulayın", function () {
    const responseData = pm.response.json();
    
    pm.expect(responseData).to.be.an('object');
    pm.expect(responseData.photoUrls).to.exist.and.to.be.an('array').and.to.have.lengthOf.at.least(1);
});
```
</details>

![Pet Ekle (Post)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/d94028d8-eeb0-463a-b676-ab3d80424819)

#### 👨🏻‍💻 Pet Bilgisi Getirme (https://petstore.swagger.io/v2/pet/12345)
***
<details>
  <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>

```javascript
pm.test("Durum kodu 200 tamam", function () {
    pm.response.to.have.status(200);
});

pm.test("Yanıt evcil hayvan ayrıntılarını içeriyor", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
    pm.expect(jsonData).to.have.property("name");
    pm.expect(jsonData).to.have.property("tags");
    pm.expect(jsonData).to.have.property("status");
});
```
</details>

![Pet Bigisi Getirme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/e42de68e-549c-4229-bbd1-6d896b8453f9)

####👨🏻‍💻 Pet Güncelleme (petName=Max) (https://petstore.swagger.io/v2/pet)
***
<details>
  <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>

```javascript
pm.test("Durum kodu 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Yanıtta bir id özelliği var", function () {
    pm.expect(pm.response.json()).to.have.property('id');
});

pm.test("Yanıtın, kimliği ve adı olan bir kategori özelliği var", function () {
    pm.expect(pm.response.json()).to.have.nested.property('category.id');
    pm.expect(pm.response.json()).to.have.nested.property('category.name');
});

pm.test("Yanıtın bir name özelliği var", function () {
    pm.expect(pm.response.json()).to.have.property('name');
});

pm.test("Yanıtta bir photoUrls özelliği var", function () {
    pm.expect(pm.response.json()).to.have.property('photoUrls');
});

pm.test("Yanıtta, kimliği ve adı olan bir etiket özelliği var", function () {
    pm.expect(pm.response.json()).to.have.nested.property('tags[0].id');
    pm.expect(pm.response.json()).to.have.nested.property('tags[0].name');
});

pm.test("Yanıtta durum özelliği var", function () {
    pm.expect(pm.response.json()).to.have.property('status');
});
```
</details>

![Pet Güncelleme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/778b9ff6-a661-4274-91d2-2a7030d25bda)

#### 👨🏻‍💻 Petlerin Listesi (https://petstore.swagger.io/v2/pet/findByStatus?status=available)
***
<details>
  <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>

```javascript
pm.test("Evcil hayvanların listelendiğini doğrula", function () {
    pm.expect(pm.response.code).to.equal(200);

    const responseData = pm.response.json();

    pm.expect(responseData.length).to.be.above(0);

    for (let i = 0; i < responseData.length; i++) {
        pm.expect(responseData[i].id).to.exist;
        pm.expect(responseData[i].name).to.be.a('string');
        pm.expect(responseData[i].status).to.be.oneOf(['available', 'pending', 'sold']);
    }
});
```
</details>

![Petlerin Listesi](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/8ada1501-2ee0-4e8f-98d9-fd6f3d0669f0)

#### 👨🏻‍💻 Petlerin Resimlerini Getirme (https://petstore.swagger.io/v2/pet/12345)
***
<details>
 <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>
 
 ```javascript
  pm.test("Pet Resimlerini Getirme Testi", function () {
      pm.expect(pm.response.text()).to.include("Pet resimleri alındı");
  });
 ```
</details>

![Pet Resimleri Getirme](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/60ede347-8875-4872-9992-24335696fdd3)

#### 👨🏻‍💻 Petlerin Bilgisi Getirme (https://petstore.swagger.io/v2/pet/12345)
***
<details>
<summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>
 
 ```javascript
pm.test("Kategori Bilgisi Doğrulama Testi", function () {
    pm.response.to.have.status(200);

    pm.response.to.have.jsonBody('category');

    var categoryInfo = pm.response.json().category;

    pm.expect(categoryInfo).to.not.be.null;

    pm.expect(categoryInfo).to.be.an('object');
    pm.expect(categoryInfo).to.have.property('id');
    pm.expect(categoryInfo).to.have.property('name'); 
    pm.expect(categoryInfo.id).to.be.a('number');
    pm.expect(categoryInfo.name).to.be.a('string');

});
```
</details>
 
![Pet Bigisi Getirme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/c07da7b0-d475-42f6-9609-5cf183950fd6)

#### 👨🏻‍💻 Pet Durumu Güncelleme (https://petstore.swagger.io/v2/pet)
***
<details>
 <summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>
 
 ```javascript
pm.test("Durum kodu 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Yanıtta bir id özelliği var", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.exist;
});

pm.test("Yanıtta bir photoUrls özelliği var", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.photoUrls).to.exist;
});

pm.test("Yanıtın bir etiket özelliği var", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.tags).to.exist;
});

pm.test("Yanıtta durum özelliği var", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.status).to.exist;
    ```
});
```
</details>

![Pet Durumunu Güncelleme (Put)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/06b1fb91-6443-4b64-982a-262243a49abc)

#### 👨🏻‍💻 Pet Etiketini Güncelleme (https://petstore.swagger.io/v2/pet)
***
<details>
<summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>
 
 ```javascript
pm.test("Durum kodu 500", function () {
    pm.response.to.have.status(500);
});
```
</details>

![Pet Etiketini Güncelleme (Put)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/f61eb13e-b579-4ef2-8618-994f7958207c)

#### 👨🏻‍💻 Kategori Listesi (https://petstore.swagger.io/v2/pet/findByStatus?status=available)
***
<details>
<summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>

```javascript
pm.test("Evcil hayvan kategori listesini başarıyla getirildiğini doğrula", function () {
    pm.expect(pm.response.code).to.equal(200);
    const responseData = pm.response.json();
    pm.expect(responseData).to.not.be.empty;
});

pm.test("Kategori özelliklerini doğrula", function () {
    const responseData = pm.response.json();

    responseData.forEach(function (pet) {
        pm.expect(pet).to.have.property('id').that.is.a('number');
        pm.expect(pet).to.have.property('name').that.is.a('string');
        pm.expect(pet).to.have.property('photoUrls').that.is.an('array');

        const tags = pet.tags;
        pm.expect(tags).to.be.an('array');

        tags.forEach(function (tag) {
            pm.expect(tag).to.have.property('id').that.is.a('number');
            pm.expect(tag).to.have.property('name').that.is.a('string');
        });

        pm.expect(pet).to.have.property('status').that.is.a('string').and.equals('available');
    });
});
```
</details>

![Kategori Listesi](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/5a8f3207-3a34-45bc-bef3-ab72b51053a2)

#### 👨🏻‍💻 Pet Silme (https://petstore.swagger.io/v2/pet/12345)
***
<details>
<summary>(<i>Testi görüntülemek için tıklayın</i>)</summary>

```javascript
const petIdToDelete = 12345;

pm.test("Evcil hayvanı başarıyla sildiğini doğrula", function () {
    pm.expect(pm.response.code).to.equal(200);
    pm.expect(pm.response.json().message).to.equal(`${petIdToDelete}`);
});
```
</details>

![Pet Silme (Delete)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/3d1e584b-4be7-4821-b7d2-288cd89a54cb)

#### Monitörü Görüntüle
***
<details>
<summary>(<i>Monitörü görüntülemek için tıklayın</i>)</summary>
 

![screencapture-web-postman-co-workspace-My-Workspace-fa8d9588-c962-4a4a-8a01-c4b4ec10f5fe-monitor-PetstoreMonitor-1ee3124f-0c8a-48d0-bbd0-bb48e2f329ea-2023-08-04-09_48_47](https://github.com/akcankaan/PetstoreAPITests/assets/63432799/3f513105-1020-4106-9dae-439796a40dd5)

</details>
