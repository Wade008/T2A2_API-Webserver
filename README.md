
# T2A2 - API Webserver Project    

**Name:** Wade Doolan  
**Student number:** 12678     

<hr>  

## R1 Identification of the problem you are trying to solve by building this particular app.  

Recipes are often written on sheets of paper or in books. Books and paper can degrade over time and are easily lost. This API was designed to provide a secure place to store and share your favourite recipes. 

<hr>  

## R2 Why is it a problem that needs solving? 

My mother-in-law is a fantastic cook but never documents her recipes or has lost a lot of them over time. When we ask her how she made a particular meal she can never remember. I thought it would be good for her and for us if she could save her recipes online, so she never forgets, and we can access the information when we want to cook the same meal. Essentially, this API can be used by other people who want to share their recipes with others and/or save their recipes in a safe place, so they can always access them.

<hr>  

## R3 Why have you chosen this database system? What are the drawbacks compared to others?

### Reason for using PostgreSQL  

The PostgreSQL relational database management system (RDBMS) was chosen for this application for the following reasons:
- It's free, open source and has a lot of community support.
- It can run on all operating systems.
- Allows user-defined data types along with primitive data types.
- Uses Structured Query Language (SQL) and is well suited to storing relational data.
- Works with any programming language, including python.
- Is ACID compliant meaning:  

    - Atomicity: database transactions are fully completed, or they fail.
    - Consistency: data consistency is ensured since changes are rolled back when a transaction fails.
    - Isolation: ensures transactions are kept separate, with previous transactions completed before the next is allowed to e processed.
    - Durability: meaning the database can be rolled back to a previous state in the case of a server failure.  

- PostgreSQL also supports JSON and flexible text searching capability.

(Digitalocean.com 2019; EDUCBA 2019; IONOS Digital Guide 2022)


### Drawbacks   

Unfortunately, not all hosting sites support PostgreSQL (IONOS Digital Guide, 2022). Moreover, query speed can be slower than some other database management systems. For example, other NoSQL databases systems might offer faster speeds, as the relational structure of a PostgreSQL can make query speed slower, especially with large amounts of data. Also, adding new fields to a PostgreSQL database can be complicated in some cases, making changes a little more difficult compared to other systems like MongoDB. Although, PostgreSQL is free and open source, it doesn't come with a warranty or liability protection like some proprietary systems do (Stuti Dhruv, 2019).


<hr>  

## R4 Identify and discuss the key functionalities and benefits of an ORM.  

An object-relational mapper (ORM) provides a layer between object-oriented programming code and relational databases, with the aim of allowing developers to interact with the underlying database without needing to write raw SQL (Liang, 2021). The SQLAlchemy library is an example of an ORM that allows a python program to communicate with a relational database, like PostgreSQL. Essentially, the ORM is responsible for shifting data between objects and a database, while ensuring the objects and database tables remain independent (Krebs, 2017).    

### Key functionalities 

Using Python and the SQLAlchemy ORM as an example, an ORM has the following key functions: 

- **Model declaration:** This involves using Python code to write classes that define both Python objects and database table metadata all at the same time. Effectively creating a blueprint of the objects and associated database table structures using Python classes.   
- **Relationship building:** This involves expanding the model declaration above and adding foreign key constructs to the relevant tables to indicate relationships between objects and the mapped tables to be created in the underlying database. A relationship function is used to indicate relationship direction and how rows of data should be dealt with when related data from another table is deleted.    
- **Instantiation of mapped classes:** Once all the relevant objects are mapped to their corresponding database tables, the ORM allows developers to instantiate the objects the same why any object is instantiated in an object-oriented programming language. For example: ``` User(colname=data, colname=data, ...) ```    
- **Querying data:** An ORM facilitates data querying using methods and functions, in place or SQL. For example, ``` query.filter(User.name == 'ed')``` is the same as ``` SELECT * FROM USERS as a WHERE a.name = 'ed'; ```  
- **Sessions including committing:** Data is added, updated and deleted from the associated database using the session object. This object contains the add(), delete() and commit() methods, among others. Ultimately, the session.commit() method executes the associated SQL after a session.add() or session.delete() has been called.  

(Sqlalchemy.org, 2022).   

### Benefits of an ORM  

The benefits associated with ORMs include:  

- ORM queries can be written regardless of the particular relational database used for the backend. If the applications needs to migrate to another database, there is no need to re-write the existing ORM queries. 
- Reduces the need for the developer to know the exact syntax of the underlying SQL.   
- ORMs can be used for any object-oriented programming languages, so they are not confined to only a few specific languages.

(EDUCBA, 2020)

<hr>  

## R5 Document all endpoints for your API.

Important note: an admin user has full read, post, update and delete in most areas of the application. A standard user can only operate on their recipes.  

### Recipe API Endpoints User registration, login, read, update and delete 

**User registration**  

- Request: POST /auth/register 

Required data: 

```json  
{
    "username":"username",
	"email": "email@mail.com",
	"password":"password",
	"name":"name",
	"phone":"0000000000",
	"dob":"yyyy-mm-dd"
}
```
Expected response:

```json
{
	"user": "username",
	"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY2NDY3NjY0NSwianRpIjoiZWIzYTdiNzYtNzJiZi00ODVlLThiM2QtNmU4NGFlNTI3MDMzIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUiLCJuYmYiOjE2NjQ2NzY2NDUsImV4cCI6MTY2NDY5MTA0NX0.bU-rHQC418KIVe3cpF5n284nucKSExtu-QUA4yGBpv0"
}

```
Authentication: 

- Password must be a string, greater than or equal to eight characters long.

Sample POST request: 

```/auth/register```

```json
{
	"username":"wade008",
	"email": "wade2@mail.com",
	"password":"123456789",
	"name":"Wade56",
	"phone":"0123456789",
	"dob":"1980-02-12"
	
}
```
Sample response: 

```json  
{
	"user": "wade008",
	"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY2NDY3NjY0NSwianRpIjoiZWIzYTdiNzYtNzJiZi00ODVlLThiM2QtNmU4NGFlNTI3MDMzIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUiLCJuYmYiOjE2NjQ2NzY2NDUsImV4cCI6MTY2NDY5MTA0NX0.bU-rHQC418KIVe3cpF5n284nucKSExtu-QUA4yGBpv0"
}
```

**User login**  

- Request: POST /auth/user/login

Required data: 

```json  
{
    "username":"username",
	"password":"password",

}
```
Expected response:

```json
{
	"user": "username",
	"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY2NDY3NjY0NSwianRpIjoiZWIzYTdiNzYtNzJiZi00ODVlLThiM2QtNmU4NGFlNTI3MDMzIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUiLCJuYmYiOjE2NjQ2NzY2NDUsImV4cCI6MTY2NDY5MTA0NX0.bU-rHQC418KIVe3cpF5n284nucKSExtu-QUA4yGBpv0"
}
```
Authentication: 

- Password must match the password in the system.

Sample POST request: 

```/auth/user/login```

```json

{
	"username":"wade008",
	"email": "wade2@mail.com",
}

```
Sample response: 

```json  
{
	"username": "wade008",
	"token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTY2NDY3NzI4OCwianRpIjoiN2Q5ZDU2NzEtMDM3Yi00YjY5LWJlZDctNDEzODA5YjA3NDkyIiwidHlwZSI6ImFjY2VzcyIsInN1YiI6IjUiLCJuYmYiOjE2NjQ2NzcyODgsImV4cCI6MTY2NDY5MTY4OH0.WUtOCpuyUe6-pdUPoocXQJ14fIz_FA9ld0yvM-YxdMo"
}

```

**User - view current user details**  

- Request: GET /auth/user/view

Required data: 

- Not applicable

Expected response:

```json
{
	"user_id": 0,
	"username": "username",
	"email": "email",
	"password": "hashed password",
	"name": "name",
	"phone": "0000000000",
	"dob": "yyyy-mm-dd"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the logged-in user can see their details.

Sample GET request: 

```/auth/user/view```

Sample response: 

```json  
{
	"user_id": 5,
	"username": "wade008",
	"email": "wade2@mail.com",
	"password": "$2b$12$ineFN/qlClSi5b2d4jyrPOzngWhYHALpVOwIUHpEzP8QVGGyTqWIO",
	"name": "Wade56",
	"phone": "0123456789",
	"dob": "1980-02-12"
}
```

**User - update details**  

- Request: PUT /auth/user/view

Required data: 

```json  
{
    "username": "username",
	"email": "email@mail.com",
	"password": "password",
	"name": "name",
	"phone": "0000000000",
	"dob": "yyyy-mm-dd"
}
```
Expected response:
- A successful update will return the user information with the updated details

```json
{
	 "username": "username",
	"email": "email@mail.com",
	"password": "hashed password",
	"name": "name",
	"phone": "0000000000",
	"dob": "yyyy-mm-dd"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the logged-in user can see their details.

Sample PUT request: 

```/auth/user/view```

```json

{
	"username": "wade008",
	"email": "wade2@mail.com",
	"password": "123456789",
	"name": "Wade Doolan",
	"phone": "0123456789",
	"dob": "1980-02-12"
}

```
Sample response: 

```json  
{
	"user_id": 5,
	"username": "wade008",
	"email": "wade2@mail.com",
	"password": "$2b$12$SZHioNf/SRYLsYceVhHGIOqg08FmcFac57Ht.iXPgUjf/x27FpCf2",
	"name": "Wade Doolan",
	"phone": "0123456789",
	"dob": "1980-02-12"
}
```
**User - delete profile**  

- Request: DELETE /auth/user/view

Required data: 

- Not applicable

Expected response:

```json
{
	"success": "User deleted successfully"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the logged-in user can delete their profile.

### Recipe API Endpoints for recipes read, post, update and delete

**View all recipes**

- Request: GET /recipes/

Required data: 

- Not applicable

Expected response:

```json

[
    {
        "owner": "owner",
        "recipe_id": 0,
        "recipe_name": " name..",
        "serves": 0,
        "instructions": "Instructions...",
        "time_required": 00.0,
        "private": bool,
        "date_added": "yyyy-mm-dd",
        "recipe_category": "category",
        "ingredient_list": [
            {
                "ingredient": "ingredient",
                "ingredient_requirements": "requirements..."
            }, ...
    
        ],
        "ratings": [
            {
                "rated_by": "user",
                "rating": 0,
                "comment": "comment"
            }, ...
        ]
    }, ...
]

```
Authentication: 

- Not required. Anyone can view the recipes in the system that are not marked as private.

Sample GET request: 

```/recipes```

Sample response: 

```json  

[
    {
        "owner": "John Mayer",
        "recipe_id": 4,
        "recipe_name": " Chicken..",
        "serves": 4,
        "instructions": "Prepare a barbecue for medium-high heat. Coat corn with 2 teaspoons oil. Season with salt and pepper...",
        "time_required": 60.0,
        "private": false,
        "date_added": "2022-09-29",
        "recipe_category": "Chicken",
        "ingredient_list": [
            {
                "ingredient": "Pasta",
                "ingredient_requirements": "250g of pasta"
            },
            {
                "ingredient": "Salt",
                "ingredient_requirements": "1/4 tablespoon of salt"
            }, ...
            
        ],
        "ratings": [
            {
                "rated_by": "Wade Doolan",
                "rating": 5,
                "comment": "Amazing"
            }, ...
            
        ]
    },...
]

```
Query string parameters:

- Parameters: *recipe_name*, *category*
- Required: both parameters are optional, and only one parameter can be used if required
- description: provides a key word search by recipe names and or recipe category containing parameter values.

Sample GET request with parameter:

``` /recipes?recipe_name=chick&category=chick ```

sample response:

```json
[
	{
		"owner": "John Mayer",
		"recipe_id": 4,
		"recipe_name": " Chicken..",
		"serves": 4,
		"instructions": "Prepare a barbecue for medium-high heat. Coat corn with 2 teaspoons oil. Season with salt and pepper...",
		"time_required": 60.0,
		"private": false,
		"date_added": "2022-09-29",
		"recipe_category": "Chicken",
		"ingredient_list": [
			{
				"ingredient": "Pasta",
				"ingredient_requirements": "250g of pasta"
			},...
		],
		"ratings": [
			{
				"rated_by": "Wade Doolan",
				"rating_id": 4,
				"rating": 5,
				"comment": "Amazing"
			},...
		]
	}, ...
	
]
```


**View one recipe**  

- Request: GET /recipes/{recipe_id}

Required data: 

- Not applicable

Expected response:

```json
{
    "owner": "owner",
    "recipe_id": 0,
    "recipe_name": " name..",
    "serves": 0,
    "instructions": "Instructions...",
    "time_required": 00.0,
    "private": bool,
    "date_added": "yyyy-mm-dd",
    "recipe_category": "category",
    "ingredient_list": [
        {
            "ingredient": "ingredient",
            "ingredient_requirements": "requirements..."
        }, ...

    ],
    "ratings": [
        {
            "rated_by": "user",
            "rating": 0,
            "comment": "comment"
        }, ...
    ]
}
```
Authentication: 

- Not required. Anyone can view a recipe in the system that is not marked as private.

Sample GET request: 

```/recipes/1```

Sample response: 

```json  
{
	"owner": "Wade Doolan",
	"recipe_id": 1,
	"recipe_name": "Bacon and Eggs",
	"serves": 2,
	"instructions": "Poach eggs in saucepan on medium heat for 6 min. Cook bacon in pan for 10 min on medium heat. Place tomato in pan after bacon has cooked for 8 min",
	"time_required": 30.0,
	"private": false,
	"date_added": "2022-09-29",
	"recipe_category": "Breakfast",
	"ingredient_list": [
		{
			"ingredient": "Eggs",
			"ingredient_requirements": "2 eggs"
		},
		{
			"ingredient": "Domestic pig (Piglet, Pork)",
			"ingredient_requirements": "2 bacon rashers"
		}...
	],
	"ratings": [
		{
			"rated_by": "John Mayer",
			"rating": 5,
			"comment": "Wow food"
		},
		{
			"rated_by": "John Mayer",
			"rating": 4,
			"comment": "Love it"
		}...
	]
}
```
**View all recipe for logged-in user**

- Request: GET /recipes/myrecipes

Required data: 

- Not applicable

Expected response:

```json
[
    {
        "owner": "owner",
        "recipe_id": 0,
        "recipe_name": " name..",
        "serves": 0,
        "instructions": "Instructions...",
        "time_required": 00.0,
        "private": bool,
        "date_added": "yyyy-mm-dd",
        "recipe_category": "category",
        "ingredient_list": [
            {
                "ingredient": "ingredient",
                "ingredient_requirements": "requirements..."
            }, ...

        ],
        "ratings": [
            {
                "rated_by": "user",
                "rating": 0,
                "comment": "comment"
            }, ...
        ]
    }, ...

]
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token).

Sample GET request: 

```/recipes/1```

Sample response: 

```json  
{
	"owner": "Wade Doolan",
	"recipe_id": 1,
	"recipe_name": "Bacon and Eggs",
	"serves": 2,
	"instructions": "Poach eggs in saucepan on medium heat for 6 min. Cook bacon in pan for 10 min on medium heat. Place tomato in pan after bacon has cooked for 8 min",
	"time_required": 30.0,
	"private": false,
	"date_added": "2022-09-29",
	"recipe_category": "Breakfast",
	"ingredient_list": [
		{
			"ingredient": "Eggs",
			"ingredient_requirements": "2 eggs"
		},
		{
			"ingredient": "Domestic pig (Piglet, Pork)",
			"ingredient_requirements": "2 bacon rashers"
		}...
	],
	"ratings": [
		{
			"rated_by": "John Mayer",
			"rating": 5,
			"comment": "Wow food"
		},
		{
			"rated_by": "John Mayer",
			"rating": 4,
			"comment": "Love it"
		}...
	]
}
```
**Post a recipe**

- Request: POST /recipes/

Required data: 

```json
{
	"recipe_name": "name",
	"serves":0,
	"instructions":"instructions...",
	"time_required":0, #in minutes
	"private": bool, #true or false
	"recipe_category": "optional"
}
```

Expected response:

```json
{
	"recipe_name": "name",
	"serves":0,
	"instructions":"instructions...",
	"time_required":0, #in minutes
	"private": bool, #true or false
	"recipe_category": "optional"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token).

Sample POST request: 

```/recipes```

```json  
{
	"recipe_name": " Chicken..",
	"serves":4,
	"instructions":"Prepare a barbecue for medium-high heat. Coat corn with 2 teaspoons oil. Season with salt and pepper...",
	"time_required":60,
	"private": true,
	"recipe_category": "Chicken"

}
```

Sample response: 

```json  
{
	"owner": "John Mayer",
	"recipe_id": 6,
	"recipe_name": " Chicken..",
	"serves": 4,
	"instructions": "Prepare a barbecue for medium-high heat. Coat corn with 2 teaspoons oil. Season with salt and pepper...",
	"time_required": 60.0,
	"private": true,
	"date_added": "2022-10-02",
	"recipe_category": "Chicken",
	"ingredient_list": [],
	"ratings": []
}
```
**Update a recipe**

- Request: PUT /recipes/{recipe_id}

Required data: 

```json
{
	"recipe_name": "name",
	"serves":0,
	"instructions":"instructions...",
	"time_required":0, #in minutes
	"private": bool, #true or false
	"recipe_category": "optional"
}
```

Expected response:

```json
{
	"recipe_name": "name",
	"serves":0,
	"instructions":"instructions...",
	"time_required":0, #in minutes
	"private": bool, #true or false
	"recipe_category": "optional",
    "ingredient_list": [
		{
			"ingredient": "ingredient",
			"ingredient_requirements": "requirement"
		},...
	],
	"ratings": [
		{
			"rated_by": "user",
			"rating": 0,
			"comment": "comment"
		},...
	]
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token).

Sample PUT request: 

```/recipes/1```

```json  
{
	"recipe_name": "Bacon and Eggs",
	"serves": 2,
	"instructions": "Poach eggs in saucepan on medium heat for 6 min. Cook bacon in pan for 10 min on medium heat. Place tomato in pan after bacon has cooked for 8 min",
	"time_required": 30.0,
	"private": false,
	"date_added": "2022-09-29",
	"recipe_category": "Breakfast"
	}
```

Sample response: 

```json  
{
	"owner": "Wade Doolan",
	"recipe_id": 1,
	"recipe_name": "Bacon and Eggs",
	"serves": 2,
	"instructions": "Poach eggs in saucepan on medium heat for 6 min. Cook bacon in pan for 10 min on medium heat. Place tomato in pan after bacon has cooked for 8 min",
	"time_required": 30.0,
	"private": false,
	"date_added": "2022-09-29",
	"recipe_category": "Breakfast",
	"ingredient_list": [
		{
			"ingredient": "Eggs",
			"ingredient_requirements": "2 eggs"
		}, ...
	],
	"ratings": [
		{
			"rated_by": "Wade Doolan",
			"rating": 4,
			"comment": "Lovely food"
		}, ...
	]
}
```
**Delete a recipe**  

- Request: DELETE /recipes/{recipe_id}

Required data: 

- Not applicable

Expected response:

```json
{
	"message": "Recipe successfully deleted from database."
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the recipe owner can delete the recipe. Admin can delete all recipes.

### Recipe API Endpoints for recipe ingredients read, post, update and delete

**View all ingredients for a recipe**

- Request: GET /recipes/{recipe_id}/ingredients 

Required data: 

- Not applicable

Expected response:

```json
[
	{
		"list_id": 0,
		"recipe": "recipe name",
		"ingredient_requirements": "requirements",
		"ingredient": "ingedient"
	}, ...
]
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any logged-in user can view the recipe ingredients, regardless of ownership.

Sample GET request: 

```/recipes/4/ingredients```

Sample response: 

```json  
[
	{
		"list_id": 15,
		"recipe": " Chicken..",
		"ingredient_requirements": "250g of pasta",
		"ingredient": "Pasta"
	},...
	
]
```
**View one ingredient for a recipe**

- Request: GET /recipes/{recipe_id}/ingredients/{list_id}

Required data: 

- Not applicable

Expected response:

```json
{
    "list_id": 0,
    "recipe": "recipe name",
    "ingredient_requirements": "requirements",
    "ingredient": "ingedient"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any logged-in user can view the recipe ingredient, regardless of ownership.

Sample GET request: 

```/recipes/1/ingredients/3```

Sample response: 

```json  
{
	"list_id": 3,
	"recipe": "Bacon and Eggs",
	"ingredient_requirements": "1 tomato",
	"ingredient": "Garden tomato"
}
```
**Post one or more ingredient for a recipe**

- Request: POST /recipes/{recipe_id}/ingredients

Required data: 

```json
[	
    {
        "ingredient": "ingredient",
        "ingredient_requirements": "requirement"
    },
    {
        "ingredient": "ingredient",
        "ingredient_requirements": "requiremwnt"
    }, ...
   
]
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the recipe owner can add ingredients to the recipe. Admin can add ingredients to all recipes.

Sample POST request: 

```/recipes/2/ingredients```

```json
[
    {
        "ingredient": "Garden onion",
        "ingredient_requirements": "Chop half a garden onion"
    }
]
```
Sample response: 

```json  
{
	"message": "Ingredients added to recipe successfully."
}
```
**Update an ingredient for a recipe**

- Request: PUT /recipes/{recipe_id}/ingredients/{list_id}

Required data: 

```json
{
	"ingredient_requirements": "updated requirement",
	"ingredient": "updated ingredient"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the recipe owner can update an ingredient for the recipe. Admin can update ingredients to all recipes.

Sample PUT request: 

```/recipes/2/ingredients/27```

```json
{
	"ingredient_requirements": "1/4 onion, chopped",
	"ingredient": "Garden Onion"
}
```
Sample response: 

```json  
{
	"list_id": 27,
	"recipe": "Toasted sandwich",
	"ingredient_requirements": "1/4 onion, chopped",
	"ingredient": "Garden onion"
}
```
**Delete an ingredient**  

- Request: DELETE /recipes/{recipe_id}/ingredients/{list_id}

Required data: 

- Not applicable

Expected response:

```json
{
	"message": "Ingredient successfully deleted from database."
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the recipe owner can delete a recipe ingredient. Admin can delete all recipe ingredients.

### Recipe API Endpoints for recipe ratings post and delete

**Post a rating for a recipe** 

- Request: POST /recipes/{recipe_id}/rating

Required data: 

```json
{
	"rating":0,
	"comment":"comment"
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any logged-in user can post a rating for any non-private recipe.

Sample POST request: 

```/recipes/1/rating```

```json
{
	"rating":5,
	"comment":"Nice"
}
```
Sample response: 

```json  
{
	"owner": "Wade Doolan",
	"recipe_id": 1,
	"recipe_name": "Bacon and Eggs",
	"serves": 2,
	"instructions": "Poach eggs in saucepan on medium heat for 6 min. Cook bacon in pan for 10 min on medium heat. Place tomato in pan after bacon has cooked for 8 min",
	"time_required": 30.0,
	"private": false,
	"date_added": "2022-09-29",
	"recipe_category": "Breakfast",
	"ingredient_list": [
		{
			"ingredient": "Eggs",
			"ingredient_requirements": "2 eggs"
		},
		{
			"ingredient": "Domestic pig (Piglet, Pork)",
			"ingredient_requirements": "2 bacon rashers"
		},
		{
			"ingredient": "Garden tomato",
			"ingredient_requirements": "1 tomato"
		},
		{
			"ingredient": "Wheat bread",
			"ingredient_requirements": "2 slices"
		}
	],
	"ratings": [
		{
			"rated_by": "John Mayer",
            "rating_id": 8,
			"rating": 5,
			"comment": "Nice"
		}
	]
}
```
**Delete a rating for a recipe**  

- Request: DELETE /recipes/{recipe_id}/rating/{rating_id}

Required data: 

- Not applicable

Expected response:

```json
{
	"message": "Rating successfully removed from the recipe."
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, only the user who posted the rating can remove it. Admin can remove all ratings.

### Recipe API Endpoints for recipe categories read, post, update and delete

**View all categories**

- Request: GET /categories

Required data: 

- Not applicable

Expected response:

```json
[
	{
		"category_id": 1,
		"category": "Breakfast"
	},
	{
		"category_id": 2,
		"category": "Brunch"
	},
	{
		"category_id": 3,
		"category": "Lunch"
	}, ...
]
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any user can get all categories.

Query string parameters:

- Parameter: *category*
- Required: parameter is optional
- description: provides a key word search for categories containing parameter value.

Sample request with parameter:

``` /categories?category=bread ```

sample response:

```json
[
	{
		"category_id": 30,
		"category": "Bread"
	}
]
```

**View one category**

- Request: GET /categories/{category_id}

Required data: 

- Not applicable

Expected response:

```json
{
    "category_id": 0,
    "category": "category"
    "recipes": [
		{
			"recipe_name": "recipe name",
			"serves": 0,
			"time_required": 0.0,
			"date_added": "yyyy-mm-dd"
		}, ...
	]
}
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any user can get one category.

Sample GET request: 

```/categories/1```

Sample response: 

```json
{
	"category_id": 1,
	"category": "Breakfast",
	"recipes": [
		{
			"recipe_name": "Bacon and Eggs",
			"serves": 2,
			"time_required": 30.0,
			"date_added": "2022-09-26"
		}
	]
}

```
**Post a new category**

- Request: POST /categories

Required data: 

```json 
{
	"category": "new category"
}
```

Expected response:

```json
{
	"category_id": 0,
	"category": "new category"
}
```
Authentication: 

- An admin user must be logged in with a current JSON Web Token (Bearer Token). Note, only admin users can post new categories.

Sample POST request: 

```/categories/```

```json
{
	"category": "BIG Breakfast"
}
```

Sample response: 

```json
{
	"category_id": 42,
	"category": "BIG Breakfast"
}
```
**Update a category**

- Request: PUT /categories/{category_id}

Required data: 

```json 
{
	"category": "update category"
}
```

Expected response:

```json
{
	"category_id": 0,
	"category": "updated category"
}
```
Authentication: 

- An admin user must be logged in with a current JSON Web Token (Bearer Token). Note, only admin users can update categories.

Sample PUT request: 

```/categories/41```

```json
{
	"category": "BIG BIG Breakfast"
}
```

Sample response: 

```json
{
	"category_id": 42,
	"category": "BIG BIG Breakfast"
}
```

**Delete a category**

- Request: DELETE /categories/{category_id}

Required data: 

- Not applicable

Expected response:

```json
{
	"message": "Category removed successfully"
}
```
Authentication: 

- An admin user must be logged in with a current JSON Web Token (Bearer Token). Note, only admin users can delete categories.

## Recipe API Endpoints for recipe ingredients read

**View all ingredients**

- Request: GET /ingredients

Required data: 

- Not applicable

Expected response:

```json
[
	{
		"ingredient_id": 1,
		"ingredient": "Angelica"
	},
	{
		"ingredient_id": 2,
		"ingredient": "Savoy cabbage"
	},
	{
		"ingredient_id": 3,
		"ingredient": "Silver linden"
	},...
]
```
Authentication: 

- User must be logged in with a current JSON Web Token (Bearer Token). Note, any user can view all ingredients.

Query string parameters:

- Parameter: *ingredient*
- Required: parameter is optional
- description: provides a key word search for ingredients containing parameter value.

Sample request with parameter:

``` /ingredients?ingredient=fish ```

sample response:

```json
[
	{
		"ingredient_id": 296,
		"ingredient": "Atlantic wolffish"
	},
	{
		"ingredient_id": 304,
		"ingredient": "Alaska blackfish"
	},
	{
		"ingredient_id": 308,
		"ingredient": "Bluefish"
	},
	{
		"ingredient_id": 318,
		"ingredient": "American butterfish"
	}...
]
```

<hr>  

## R6 An ERD for your app.

The Entity Relationship Diagram (ERD) for the recipe API is shown below: 

Please note, this ERD can also be accessed online here: https://lucid.app/lucidchart/7c50beef-7db7-450e-86e9-3842b93b88d5/edit?viewport_loc=-77%2C-179%2C1729%2C1159%2C0_0&invitationId=inv_71615ea1-65e1-4a71-8844-eb8556fd56f8# 


![Recipe API ERD](./docs/Recipe_API_ERD.png)

<hr>  

## R7 Detail any third party services that your app will use.  

The recipe app uses data from two third party services including:

- The list of 40 recipe categories obtained from (Myfoodbook.com.au, 2022).  

- The list of 907 ingredients obtained from (Alexandra, 2018). 

The app also uses the following packages: 

- autopep8==1.7.0
- bcrypt==4.0.0
- click==8.1.3- 
- Flask==2.2.2
- Flask-Bcrypt==1.0.1
- Flask-JWT-Extended==4.4.4
- flask-marshmallow==0.14.0
- Flask-SQLAlchemy==2.5.1
- greenlet==1.1.3
- itsdangerous==2.1.2
- Jinja2==3.1.2
- MarkupSafe==2.1.1
- marshmallow==3.18.0
- marshmallow-sqlalchemy==0.28.1
- numpy==1.23.3
- packaging==21.3
- pandas==1.4.4
- psycopg2-binary==2.9.3
- pycodestyle==2.9.1
- pyJWT==2.4.0
- pyparsing==3.0.9
- python-dateutil==2.8.2
- python-dotenv==0.21.0
- pytz==2022.2.1
- six==1.16.0
- SQLAlchemy==1.4.41
- toml==0.10.2
- Werkzeug==2.2.2

(PyPI, 2022)

## R8 Describe your projects models in terms of the relationships they have with each other.

The recipe API has the following entities:

- Recipe  
- User  
- Ingredient 
- Category  

The API also requires the following linking tables

- Ingredient_list
- Rating


### Relationships

- A Recipe requires many ingredients. 
- An Ingredient can have many recipes associated with it.
- A Recipe can only have one category associated with it.
- A Category can have many recipes associated with it.
- A User can post many recipes.
- A User can rate many recipes, while a recipe can have many ratings.

The many-to-many relationship between the Recipe and Ingredient objects is addressed by using a linking table, Ingredient_list. And the many-to-many relationship between the Recipe and User objects in relation to ratings is addressed by using a linking table, Rating. This is addressed further in R9 below.

Each object is addresses in more detail below.

#### Recipe

The API's Recipe model represents a parent object that is related to children models, IngredientList and Rating. 

- There can be many IngredientList objects related to one Recipe object. An IngredientList object can be deleted without needing to remove the associated Recipe object. However, if a Recipe object is deleted, then all associated IngredientList objects need to be deleted.

- There can be many Rating objects related to one Recipe object. A Rating object can be deleted without needing to a related Recipe object. However, if a Recipe object is deleted, then all associated Rating objects need to be deleted.  

The Recipe model also represents a child object that is related to the User and Category models. 

 - There can be many Recipe objects related to one User object. A Recipe object can be deleted without needing to remove the associated User object. However, if a User object is deleted, then all associated Recipe objects need to be deleted.

 - There can be many User objects related to one Category object. A Recipe object can be deleted without needing to remove the associated Category object. However, if a Category object is deleted, then the associated Recipe object can remain as it is not necessary for the Recipe object to have a Category linked to it.  

 #### User model  

 The User model represents a parent object related to children models, Recipe and Rating. 

- As mentioned above, the User model has a one-to-many relationship with the Recipe model. Importantly, if a user is deleted then the associated Recipe objects also need to be deleted. 

- There can be many Rating objects associated with the User model. If a User object is deleted, then all associated Rating objects will be deleted.

#### Rating model  

The Rating model represents a child in relation to the Recipe and User models. This model forms a linking object between the User and Recipe models to manage the many-many relationship between the Recipe and User models. A rating can be deleted and will have no impact on the User and Recipe models.

#### Ingredient  

The Ingredient model is a parent to the IngredientList model. That is, one-to-many relationship between the Ingredient and IngredientList models. If an ingredient is removed from the Ingredient model, it will cascade to delete all associated IngredientList objects. 


#### IngredientList model  

The IngredientList model represents a child object in relation to the Recipe and Ingredient models. An IngredientList onject can be removed from the model without impacting the related Parent objects. This model forms a linking object between the Recipe and Ingredient models to manage the many-many relationship between the Recipe and Ingredient models.  


#### Category model   

As mentioned before, the Category model is a parent object to the Recipe object. A Category object can be deleted without impacting the related Recipe object, as a Recipe object can exist without an associated Category object.

<hr>  

## R9 Discuss the database relations to be implemented in your application.

The recipe application database relationships are outlined below.

As previously mentioned, the application's database is comprised of six tables. These include:

- Recipes 
- Users  
- Ratings 
- Ingredient_list
- Ingredients 
- Categories 

These tables and their relationships are shown in the database modelling section of the Recipe Entity Relationship Diagram (ERD) (refer to the crow's foot diagram):
https://lucid.app/lucidchart/7c50beef-7db7-450e-86e9-3842b93b88d5/edit?viewport_loc=-77%2C-179%2C1729%2C1159%2C0_0&invitationId=inv_71615ea1-65e1-4a71-8844-eb8556fd56f8# 

The recipe application has the following implemented relationships:  

- **Users and recipes:** The users table is associated with the recipe table in a one-to-many relationship. That is, the primary key of the users tables is represented as a foreign key in the recipes table. This foreign key constraint is required (cannot be null) as a recipe must be owned by a user. If a user is removed from the system the associated recipes must also be removed. 
- **Ratings and recipes:** The ratings table represents a linking table between recipes and users. A recipe can have many ratings and therefore the recipes table primary key is represented as a foreign key on the ratings table, with this key required (not nullable). A rating can be removed without affecting the recipes tables. 
- **Ratings and Users:** Only users can rate a recipe. As such a relationship between users and ratings has been implemented in a one-to-many fashion. That is, the primary key from the users table is a foreign key constraint on the ratings table and again this is not nullable. If a user is removed from the system, then the associated ratings must also be removed. 
- **Recipes and ingredient_list:** The ingredient_list table represents a linking table between the recipes and ingredients table. A recipe can have many ingredients; therefore, the recipes table primary keys is also a foreign key on the ingredient_list table, with this key required (not nullable). An ingredient can be removed without affecting the recipe table, however, if a recipe is deleted the associated ingredient_list items must also be removed to maintain data integrity.
- **Ingredients and ingredient_list:** As previously mentioned, the ingredient_list table is link between the recipes and ingredients tables. One ingredient can be related to many ingredient_list items. If an ingredient is removed form the database, all associated ingredient_list items must also be removed. 
- **Categories and recipes:** The categories table shows that one category can relate to many recipes. The primary key of the categories table is represented as a foreign key in the recipes table. Note, it is not required for a recipe have a category; therefore, the category_id foreign key in the recipes table can be null. If a category is removed from the database, the associated recipes will not be removed. 

Important note: in order to maintain data integrity in the database, a standard user is not able to add, delete or update ingredients in the ingredient table. Nor is a standard user able to add, delete or update categories in the categories table. The categories table will be preloaded with 40 unique categories. And the ingredients table is preloaded with 907 unique ingredients. Only an admin user is able to make changes to the categories tables, while the ingredients table can not be altered.

<hr>  

## R10 Describe the way tasks are allocated and tracked in your project.

Trello was used to allocate tasks and track the Recipe API project.

![Recipe API Trello Board](./docs/Recipe%20API%20Trello%20Board.png)


The full implementation plan is available in Trello (link below):
https://trello.com/invite/b/pNb7bhKr/6e627b4c3d44b35d748e11c835f8f3c3/recipe-api-implementation 



<hr>  

## References  

Alexandra (2018). Generic Food Database. [online] Data.world. Available at: https://data.world/alexandra/generic-food-database [Accessed 20 Sep. 2022].

Digitalocean.com. (2019). ACID Compliance :: DigitalOcean Documentation. [online] Available at: https://docs.digitalocean.com/glossary/acid/#:~:text=PostgreSQL%20is%20ACID%2Dcompliant.,order%20to%20keep%20data%20consistent. [Accessed 30 Sep. 2022].

Documenting APIs. (2022). Putting it all together. [online] Available at: https://idratherbewriting.com/learnapidoc/docapis_finished_doc_result.html [Accessed 2 Oct. 2022].

EDUCBA. (2019). What is PostgreSQL? | Features | Advantages and Disadvantages. [online] Available at: https://www.educba.com/what-is-postgresql/ [Accessed 30 Sep. 2022].

EDUCBA. (2020). What is ORM? | How ORM Works? | A Quick Glance of ORM Features. [online] Available at: https://www.educba.com/what-is-orm/ [Accessed 30 Sep. 2022].

IONOS Digital Guide (2022). PostgreSQL: a closer look at the object-relational database management system. [online] IONOS Digital Guide. Available at: https://www.ionos.com/digitalguide/server/know-how/postgresql/ [Accessed 30 Sep. 2022].

Krebs, B. (2017). SQLAlchemy ORM Tutorial for Python Developers. [online] Auth0 - Blog. Available at: https://auth0.com/blog/sqlalchemy-orm-tutorial-for-python-developers/ [Accessed 30 Sep. 2022].

Liang, M. (2021). Understanding Object-Relational Mapping: Pros, Cons, and Types. [online] AltexSoft. Available at: https://www.altexsoft.com/blog/object-relational-mapping/#:~:text=application%20development%20efforts.-,What%20is%20an%20ORM%3F,boilerplate%20and%20speeding%20development%20time. [Accessed 30 Sep. 2022].

Myfoodbook.com.au. (2022). Recipe Categories. [online] Available at: https://myfoodbook.com.au/categories [Accessed 17 Sep. 2022].

PyPI. (2022). pip. [online] Available at: https://pypi.org/project/pip/ [Accessed 2 Oct. 2022].

Sqlalchemy.org. (2022). ORM Quick Start — SQLAlchemy 1.4 Documentation. [online] Available at: https://docs.sqlalchemy.org/en/14/orm/quickstart.html [Accessed 30 Sep. 2022].

Stuti Dhruv (2019). Pros and Cons of using PostgreSQL for Application Development. [online] Aalpha. Available at: https://www.aalpha.net/blog/pros-and-cons-of-using-postgresql-for-application-development/ [Accessed 30 Sep. 2022].









