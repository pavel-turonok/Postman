
# :large_orange_diamond: HW_1
### _Создать запросы в Postman_
```
Protocol: http
IP: 162.55.220.72
Port: 5005
```
____________________

### EP_1
```
Method: GET
EndPoint: /get_method
request url params: 
 name: str
 age: int
```
### _response_
```
[
 “Pavel”,
 “24”
]
```
____________________

### EP_2
```
Method: POST
EndPoint: /user_info_3
request form data: 
 name: str
 age: int
 salary: int
```
### _response_
```
{
 "age": "24",
 "family": {"children": [
            ["Alex", 24],
            ["Kate", 12]
          ],
        "u_salary_1_5_year": 4000
    },
    "name": "Pavel",
    "salary": 5000
}
```
____________________

### EP_3
```
Method: GET
EndPoint: /object_info_1
request url params: 
 name: str
 age: int
 weight: int
```
### _response_
```
{
 "age": 24,
 "daily_food": 0.72,
 "daily_sleep": 150.0,
 "name": "Pavel"
}
```
____________________

### EP_4
```
Method: GET
EndPoint: /object_info_2
request url params: 
 name: str
 age: int
 salary: int
```
### _response:_
```
{
    "person": {
        "u_age": 24,
        "u_name": ["Pavel",1000,24],
        "u_salary_5_years": 21000.0
    },
    "qa_salary_after_1.5_year": 16500.0,
    "qa_salary_after_12_months": 13500.0,
    "qa_salary_after_3.5_years": 19000.0,
    "qa_salary_after_6_months": 10000,
    "start_qa_salary": 5000
}
```
____________________

### EP_5
```
Method: GET
EndPoint: /object_info_3
request url params: 
 name: str
 age: int
 salary: int
```
### _response_
```
{
    "age": "24",
    "family": {
        "children": [
            ["Alex", 24],
            ["Kate", 12]
        ],
        "pets": {"cat": {"age": 3,"name": "Sunny"},
                 "dog": {"age": 4, "name": "Luky"}
        },
        "u_salary_1_5_year": 20000
    },
    "name": "Pavel",
    "salary": 5000
}
```
____________________

### EP_6
```
Method: GET
EndPoint: /object_info_4
request url params: 
 name: str
 age: int
 salary: int
```
### _response_
```
{
    "age": 24,
    "name": "Pavel",
    "salary": [5000, "10000", "15000"]
}
```
____________________

### EP_7
```
Method: POST
EndPoint: /user_info_2
request form data: 
 name: str
 age: int
 salary: int
```
### _ response_
```
{
    "person": {"u_age": 24, "u_name": ["Pavel", 5000, 24],"u_salary_5_years": 21000},
    "qa_salary_after_1.5_year": 16500,
    "qa_salary_after_12_months": 13500,
    "qa_salary_after_3.5_years": 19000,
    "qa_salary_after_6_months": 10000,
    "start_qa_salary": 5000
}
```
____________________        

# :large_orange_diamond: HW_2
### EP_1
http://162.55.220.72:5005/first
1. Отправить запрос.
2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
3. Проверить, что в body приходит правильный string.
```
pm.test("Body is correct", function () {
    pm.response.to.have.body("This is the first responce from server!ss");
});
```
_____________________________________

### EP_2
1. Отправить запрос.
2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
3. Спарсить response body в json
```
let response_Json = pm.response.json();
```
4. Проверить, что name в ответе равно name s request (name вбить руками.)
```
pm.test("Name is Pavel", function () {
    pm.expect(response_Json.name).to.eql("Pavel");
});
```
5. Проверить, что age в ответе равно age s request (age вбить руками.)
```
pm.test("Age is 24", function () {
    pm.expect(response_Json.age).to.eql('24');
});
```
6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
```
pm.test("Salary is 5000", function () {
    pm.expect(response_Json.salary).to.eql(5000);
});
```
7. Спарсить request.
```
let req_data = request.data;
```
8. Проверить, что name в ответе равно name s request (name забрать из request.)
```
let res_name = req_data.name;
let req_name = response_Json.name;
pm.test("Name res eql name req", function () {
    pm.expect(res_name).to.eql(req_name);
});
```
9. Проверить, что age в ответе равно age s request (age забрать из request.)
```
let res_age = req_data.age;
let req_age = response_Json.age;
pm.test("Age res eql age req", function () {
    pm.expect(req_age).to.eql(res_age);
});
```
10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```
let res_salary = +req_data.salary;
let req_salary = +response_Json.salary;
pm.test("Salary res eql salary req", function () {
    pm.expect(req_salary).to.eql(res_salary);
});
```
11. Вывести в консоль параметр family из response.
```
let family = jsonData.family
console.log('Family -- ', response_Json.family)
```
12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
```   
let req1_salary = +req_data.salary
let resp_salary_1_5_years = response_Json.family.u_salary_1_5_year
pm.test("req_salary_1_5 eql salary * 4", function () {
pm.expect(req1_salary*4).to.eql(resp_salary_1_5_years);
});
```
_______________________________________

### EP_3
http://162.55.220.72:5005/object_info_3
1. Отправить запрос.
2. Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```
let resp_Json = pm.response.json();
```    
4. Спарсить request.
```
let req = pm.request.url.query.toObject(); 
```    
5. Проверить, что name в ответе равно name s request (name забрать из request.)
```    
pm.test("Name from req = name from resp", function () {
pm.expect(resp_Json.name).to.eql(req.name);
});
```
6. Проверить, что age в ответе равно age s request (age забрать из request.)
```
pm.test("Age from req = age from resp", function () {
pm.expect(resp_Json.age).to.eql(req.age);
});
```
7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
```
pm.test("Salary from req = salary from resp", function () { 
pm.expect(+resp_Json.salary).to.eql(+req.salary);
});
```
8. Вывести в консоль параметр family из response.
```
console.log(resp_Json.family)
```
9. Проверить, что у параметра dog есть параметры name.
```
pm.test("name is Luky", function () { 
pm.expect(resp_Json.family.pets.dog).to.have.property("name");
});
```
10. Проверить, что у параметра dog есть параметры age.
```
pm.test("name is Luky", function () { 
pm.expect(resp_Json.family.pets.dog).to.have.property("age");
});
```
11. Проверить, что параметр name имеет значение Luky.
```
pm.test("name is Luky", function () { 
pm.expect(resp_Json.family.pets.dog.name).to.eql("Luky");
});
```
12. Проверить, что параметр age имеет значение 4.
```
pm.test("Age is 4", function () { 
pm.expect(resp_Json.family.pets.dog.age).to.eql(4);
});
```
_______________________________________

### EP_4
http://162.55.220.72:5005/object_info_4
1. Отправить запрос.
2. Статус код 200
```
pm.test("Status code is 200", function () {
pm.response.to.have.status(200);
});
```
3. Спарсить response body в json.
```
let resp_in_json = pm.response.json();
```
4. Спарсить request.
```
let req = pm.request.url.query.toObject(); 
```
5. Проверить, что name в ответе равно name s request (name забрать из request.)
```
pm.test("Name from req = name from resp", function () {
pm.expect(resp_in_json.name).to.eql(req.name);
});
```
6. Проверить, что age в ответе равно age из request (age забрать из request.)
```
pm.test("Age from req = age from resp", function () {
pm.expect(resp_in_json.age).to.eql(+req.age);
});
```
7. Вывести в консоль параметр salary из request.
```
console.log(req.salary)
```
8. Вывести в консоль параметр salary из response.
```
console.log(resp_in_json.salary)
```
9. Вывести в консоль 0-й элемент параметра salary из response.
```
console.log(resp_in_json.salary[0])
```
10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
```
console.log(resp_in_json.salary[1])
```
11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
```
console.log(resp_in_json.salary[2])
```
12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
```
pm.test("0 salary element = salary from req", function () {
pm.expect(resp_in_json.salary[0]).to.eql(+req.salary);
});
```
13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
```
pm.test("1 salary element = salary from req", function () {
pm.expect(+resp_in_json.salary[1]).to.eql(req.salary*2);
});
```
14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
```
pm.test("1 salary element = salary from req", function () {
pm.expect(+resp_in_json.salary[2]).to.eql(req.salary*3);
});
```
15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name
19. Передать в окружение переменную age
20. Передать в окружение переменную salary
```
pm.environment.set("name", "Pavel");
pm.environment.set("age", 24);
pm.environment.set("salary", 5000);
```    
21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
```
for (let i in resp_in_json.salary) {
console.log(i)
	};
```
_______________________________________

### EP_5
http://162.55.220.72:5005/user_info_2
1. Вставить параметр salary из окружения в request
2. Вставить параметр age из окружения в age
3. Вставить параметр name из окружения в name
4. Отправить запрос.
5. Статус код 200
6. Спарсить response body в json.
```
let resp_body = pm.response.json();
```    
7. Спарсить request.
```
let req_body = request.data
```  
8. Проверить, что json response имеет параметр start_qa_salary
```
pm.test("Start qa salary property", function () {
pm.expect(resp_body).to.have.property("start_qa_salary");
});
```
9. Проверить, что json response имеет параметр qa_salary_after_6_months
```
pm.test("qa salary 6 months property", function () {
pm.expect(resp_body).to.have.property("qa_salary_after_6_months");
});
```
10. Проверить, что json response имеет параметр qa_salary_after_12_months
```
pm.test("qa salary 12 months property", function () {
pm.expect(resp_body).to.have.property("qa_salary_after_12_months");
});
```
11. Проверить, что json response имеет параметр qa_salary_after_1.5_year
```
pm.test("qa salary 1.5 months property", function () {
pm.expect(resp_body).to.have.property("qa_salary_after_1.5_year");
});
```
12. Проверить, что json response имеет параметр qa_salary_after_3.5_years
```
pm.test("qa salary 3.5 months property", function () {
pm.expect(resp_body).to.have.property("qa_salary_after_3.5_years");
});
```
13. Проверить, что json response имеет параметр person
```
pm.test("person property", function () {
pm.expect(resp_body).to.have.property("person");
});
```
14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)
```    
pm.test("Start qa salary = salary", function () {
pm.expect(resp_body.start_qa_salary).to.eql(+req_body.salary);
});
```
15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)
```
pm.test("Qa 6 months salary = salary", function () {
pm.expect(resp_body.qa_salary_after_6_months).to.eql(+req_body.salary*2);
});
```
16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)
```
pm.test("Qa 12 months salary = salary", function () {
pm.expect(resp_body.qa_salary_after_12_months).to.eql(+req_body.salary*2.7);
});
```
17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)
```
pm.test("Qa 1.5 year salary = salary", function () {
pm.expect(resp_body.qa_salary_after_1_5_year).to.eql(+req_body.salary*3.3);
});
```
18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)
```
pm.test("Qa 3.5 year salary = salary", function () {
pm.expect(+req_body.salary*3.8).to.eql(resp_body.qa_salary_after_3_5_year);
});
```
19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)
```
pm.test("U_name = salary", function () {
pm.expect(resp_body.person.u_name[1]).to.eql(+req_body.salary);
});
```
20. Проверить, что что параметр u_age равен age из request (age забрать из request.)
```
pm.test("U_age = age", function () {
pm.expect(resp_body.person.u_age).to.eql(+req_body.age);
});
```
21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)
```
pm.test("U_salary_5_years = salary", function () {
pm.expect(resp_body.person.u_salary_5_years).to.eql(+req_body.salary*4.2);
});
```
22. *** Написать цикл который выведет в консоль по порядку элементы списка из параметра person.
```
for (let i in resp_body.person) {
console.log(i)
};
```
____________________        

# :large_orange_diamond: HW_3
### EP_1
http://162.55.220.72:5005/first

необходимо залогиниться

POST

http://162.55.220.72:5005/login

login : str (кроме /)

password : str

Приходящий токен необходимо передать во все остальные запросы.
```
let resp_token = pm.response.json().token;
pm.environment.set("token", resp_token);
```

дальше все запросы требуют наличие токена.

## EP_2
http://162.55.220.72:5005/user_info

req. (RAW JSON)

POST

age: int

salary: int

name: str

auth_token

```
resp.
{'start_qa_salary':salary,
 'qa_salary_after_6_months': salary * 2,
 'qa_salary_after_12_months': salary * 2.9,
 'person': {'u_name':[user_name, salary, age],
                                'u_age':age,
                                'u_salary_1.5_year': salary * 4}
                                }
```
Тесты:
1) Статус код 200
```
pm.test("Status code is 200", function () {
pm.response.to.have.status(200);
});
```
2) Проверка структуры json в ответе.
```
pm.test("Resp is JSON", function () {
pm.response.to.be.json;
});
let req_info = JSON.parse(request.data);
let user_info = pm.response.json();
pm.test("Проверка наличия параметра 'person'", function () {
    pm.expect(user_info).to.have.property("person");
});
pm.test("Проверка наличия параметра 'start_qa_salary'", function () {
    pm.expect(user_info).to.have.property("start_qa_salary", 5000);
});    
pm.test("Проверка наличия параметра 'qa_salary_after_6_months'", function () {
    pm.expect(user_info).to.have.property("qa_salary_after_6_months", 10000);
});
pm.test("Проверка наличия параметра 'qa_salary_after_12_months'", function () {
    pm.expect(user_info).to.have.property("qa_salary_after_12_months", 14500);
});   
pm.test("Проверка структуры 'person'", function () {
    pm.expect(user_info.person).to.have.property("u_age", 24);
    pm.expect(user_info.person).to.have.property("u_name");
    pm.expect(user_info.person).to.have.property("u_salary_1_5_year", 20000);
});
pm.test("Проверка структуры 'u_name'", function () {
    pm.expect(user_info.person.u_name[0]).to.eql ("Pavel");
    pm.expect(user_info.person.u_name[1]).to.eql (5000);
    pm.expect(user_info.person.u_name[2]).to.eql (24);
});       
```
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
```
pm.test("start_qa_salary", function () {
pm.expect(user_info.start_qa_salary).to.eql(req_info.salary);
});
pm.test("qa_salary_after_6_months", function () {
pm.expect(user_info.qa_salary_after_6_months).to.eql(req_info.salary*2);
});
pm.test("qa_salary_after_12_months", function () {
    pm.expect(user_info.qa_salary_after_12_months).to.eql(req_info.salary*2.9);
});
pm.test("u_salary_1_5_year", function () {
    pm.expect(user_info.person.u_salary_1_5_year).to.eql(req_info.salary*4);
});
```
4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary запроса http://162.55.220.72:5005/get_test_user
```
let salary_1_5 = user_info.person.u_salary_1_5_year;
pm.environment.set("salary_1_5", "salary_1_5");
```
===================

## EP_3 
http://162.55.220.72:5005/new_data

req.

POST

age: int

salary: int

name: str

auth_token
```
Resp.
{'name':name,
  'age': int(age),
  'salary': [salary, str(salary*2), str(salary*3)]}
```
Тесты:
1) Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2) Проверка структуры json в ответе.
```
pm.test("Resp is JSON", function () {
    pm.response.to.be.json;
});
```
3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке правильности результата перемножения на коэффициент.
```
let req_sal = request.data;
let user_sal = pm.response.json();
pm.test("salary_0", function () {
    pm.expect(user_sal.salary[0]).to.eql(+req_sal.salary);
});
pm.test("salary_1", function () {
    pm.expect(+user_sal.salary[1]).to.eql(req_sal.salary*2);
});
pm.test("salary_2", function () {
    pm.expect(+user_sal.salary[2]).to.eql(req_sal.salary*3);
});
```
4) проверить, что 2-й элемент массива salary больше 1-го и 0-го
```   
    let salary_2_1 = user_sal.salary[2] > user_sal.salary[1];
    let salary_2_0 = user_sal.salary[2] > user_sal.salary[0];
pm.test("salary_2 > salary_1", function () {
    pm.expect(salary_2_1).to.eql(true);
});
pm.test("salary_2 > salary_0", function () {
    pm.expect(salary_2_0).to.eql(true);
});
```
===================
## EP_4  
http://162.55.220.72:5005/test_pet_info

req.

POST

age: int

weight: int

name: str

auth_token

```
Resp.
{'name': name,
 'age': age,
 'daily_food':weight * 0.012,
 'daily_sleep': weight * 2.5}
```

Тесты:
1) Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2) Проверка структуры json в ответе.
```
pm.test("Resp is JSON", function () {
    pm.response.to.be.json;
});
```
3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке правильности результата перемножения на коэффициент.
```
let req = request.data;
let resp = pm.response.json();

    pm.test("daily_food check", function () {
    pm.expect(resp.daily_food).to.eql(req.weight*0.012);
});
    pm.test("daily_sleep check", function () {
    pm.expect(resp.daily_sleep).to.eql(req.weight*2.5);
});
```
===================

## EP_5  
http://162.55.220.72:5005/get_test_user

req.

POST

age: int

salary: int

name: str

auth_token
```
Resp.
{'name': name,
 'age':age,
 'salary': salary,
 'family':{'children':[['Alex', 24],['Kate', 12]],
 'u_salary_1.5_year': salary * 4}
  }
```
Тесты:
1) Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2) Проверка структуры json в ответе.
```
pm.test("Resp is JSON", function () {
    pm.response.to.be.json;
});
```
3) Проверить что занчение поля name = значению переменной name из окружения
```
let resp = pm.response.json();
pm.test("name", function () {
    pm.expect(resp.name).to.eql(pm.environment.get("name"));
});
```
4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе значению поля age
```
let req = request.data;
pm.test("age", function () {
    pm.expect(resp.age).to.eql(req.age);
});
```
===================

## EP_6  
http://162.55.220.72:5005/currency

req.

POST

auth_token

Resp. Передаётся список массив объектов.
```
[
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
…
{"Cur_Abbreviation": str,
 "Cur_ID": int,
 "Cur_Name": str
}
]
```
Тесты:
1) Можете взять любой объект из присланного списка, используйте js random.
В объекте возьмите Cur_ID и передать через окружение в следующий запрос.
```   
let resp = pm.response.json();
pm.environment.set("curr_code", Math.floor(Math.random()*resp.length));
```
 ===================

## EP_7 
http://162.55.220.72:5005/curr_byn

req.

POST

auth_token

curr_code: int

Resp.
```
{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
}
```
Тесты:
1) Статус код 200
```
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
2) Проверка структуры json в ответе.
```
pm.test("Resp is JSON", function () {
    pm.response.to.be.json;
});
```
