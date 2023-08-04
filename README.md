👨🏻‍💻 Pet ekle (petName=Mia) 

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

![Pet Ekle (Post)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/d94028d8-eeb0-463a-b676-ab3d80424819)


👨🏻‍💻 Pet Bilgisi Getirme (https://petstore.swagger.io/v2/pet/12345)

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

![Pet Bigisi Getirme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/e42de68e-549c-4229-bbd1-6d896b8453f9)

👨🏻‍💻 Pet Güncelleme (petName=Max) (https://petstore.swagger.io/v2/pet)

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

![Pet Güncelleme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/778b9ff6-a661-4274-91d2-2a7030d25bda)

👨🏻‍💻 Petlerin Listesi (https://petstore.swagger.io/v2/pet/findByStatus?status=available)

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

![Petlerin Listesi](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/8ada1501-2ee0-4e8f-98d9-fd6f3d0669f0)

👨🏻‍💻 Petlerin Resimlerini Getirme (https://petstore.swagger.io/v2/pet/12345)

pm.test("Pet Resimlerini Getirme Testi", function () {
    pm.expect(pm.response.text()).to.include("Pet resimleri alındı");
});

![Pet Resimleri Getirme](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/60ede347-8875-4872-9992-24335696fdd3)

👨🏻‍💻 Petlerin Bilgisi Getirme (https://petstore.swagger.io/v2/pet/12345)

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

![Pet Bigisi Getirme (Get)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/c07da7b0-d475-42f6-9609-5cf183950fd6)

👨🏻‍💻 Petlerin Bilgisi Getirme (https://petstore.swagger.io/v2/pet)

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
});

![Pet Durumunu Güncelleme (Put)](https://github.com/akcankaan/Postman-API-Test-Petstore-swagger.io/assets/63432799/06b1fb91-6443-4b64-982a-262243a49abc)
