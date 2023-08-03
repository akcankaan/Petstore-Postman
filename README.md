👨🏻‍💻 (petName=Mia) Pet ekle

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

