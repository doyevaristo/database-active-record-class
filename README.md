Database active record
===================

> **Available fields:**

> - This library completly  is written for composer package
> - This will works with vendor autoload
> - Codeigniter active record class interface used
> - These library use simple and fast of

Let's start!
----

Database Configuration
---

First let's start with the database settings.

database configuration files in the **Db** folders -> **config.php**


```sh
$current = 'mysql:connect1';

$db = array(
	'mysql' => array(
		'connect1' => array(
			'hostname' => 'localhost',
			'username' => 'root',
			'password' => '',
			'database' => '',
			'dbprefix' => ''

		)
	)
);
```

The **$current** variable is the driver you want to use as the active and allows you to use the database connection.

**Example:**

Up when I want to define a second database connection settings you need to do the following.

```sh
	'connect2' => array(
			'hostname' => 'localhost',
			'username' => 'root',
			'password' => '',
			'database' => '',
			'dbprefix' => ''

		)
		
```

and my **$current** variable have been:

```sh
$current = 'mysql:connect2'; 
```

We can define the connection as we want it that way.

> **Note:**
> ***mysql*** needs to be defined for the identification of the considered prospective.

We first make the database connection
---


Add our workspace our library
```sh
use Db\Query as DB;
```

We install the library and also have set a alias. I chose the DB alias.

**A simple database query:**

```sh
DB::select('*');
DB::get('example_table');
```

We questioned directly above our table without specifying any criteria query.
We can do the same query in the following way:

```sh
DB::select('*')->get('example_table');
```

**SELECT:**
--

**Use 1:**
```sh
DB::select('*')->get('example_table');
```

**Use 2:**
```sh
DB::select('examle_type.*')->get('example_type');
```
**Use 3:**
```sh
DB::select('example_type.id');
DB::select('example_type.name')->get('example_type');
```
<br />
**select_max():**

```sh
$result = DB::select_max('id')->get('example_type');

echo $result->row()->id;
```
<br />
**select_min():**

```sh
$result = DB::select_max('id')->get('example_type');

echo $result->row()->id;
```
<br />
**select_avg():**

```sh
$result = DB::select_avg('age')->get('example_type');

echo $result->row()->age;
```
<br />
**select_sum():**

```sh
$result = DB::select_sum('total')->get('example_type');

echo $result->row()->total;
```
<br />
**distinct():**

```sh
$result = DB::distinct('city')->get('example_type');

echo $result->row()->city;
```
**FROM:**
--
**from():**

```sh
$result = DB::select('*')->from('example_table')->get();

echo $result->row()->total;
```

**WHERE**
--
```sh
$result = DB::where('city','Istanbul')->get('users');

print_r $result->result_array();
```

Where you can pass parameters to the method in 3 ways.

**Method 1:**
```sh
$result = DB::where('city !=','Istanbul')->get('users');

print_r $result->result_array();
```

```sh
$result = DB::where('age >',19)->get('users');

print_r $result->result_array();
```

```sh
$result = DB::where('age <',19)->get('users');

print_r $result->result_array();
```
```sh
$result = DB::where('age <>',18)->get('users');

print_r $result->result_array();
```

```sh
$result = DB::where('city','Istanbul')->get('users');

print_r $result->result_array();
```

**Method 2:**
```sh
$result = DB::where(array('city' => 'Istanbul'))->get('users');

print_r $result->result_array();
```

```sh
$result = DB::where(array('age >' => 19))->get('users');

print_r $result->result_array();
```

```sh
$result = DB::where(array('age <' => 19))->get('users');

print_r $result->result_array();
```
```sh
$result = DB::where(array('age <>' => 18))->get('users');

print_r $result->result_array();
```

**Method 3:**
```sh
$result = DB::where("city => 'Istanbul'")->get('users');

print_r $result->result_array();
```

suc as.

If we want we can create a query like:
```sh
$result = DB::where('id',1)
	->where(array('city' => 'Istanbul'))
	->where("age <> '18'")->get('users');

print_r $result->result_array();
```
<br />
**or_where():**
```sh
$result = DB::where('id',1)->or_where('age',18)->get('users');
```
<br />
**where_in():**
```sh
$result = DB::where_in('age',18)->get('users');
```
a different use:
```sh
$result = DB::where_in('age',array(18,20,22,23))->get('users');
```
> **Note:**
> This combination can be used on all **where_in**

<br />
**or_where_in():**
```sh
$result = DB::where('city','Istanbul')->or_where_in('age',18)->get('users');
```
<br />
**where_not_in():**
```sh
$result = DB::where_not_in('age',18)->get('users');
```
<br />
**or_where_not_in():**
```sh
$result = DB::where('city','Istanbul')->or_where_not_in('age',18)->get('users');
```
<br />

**or_where_not_in():**
```sh
$result = DB::where('city','Istanbul')->or_where_not_in('age',18)->get('users');
```

<br />

**or_where_not_in():**
```sh
$result = DB::where('city','Istanbul')->or_where_not_in('age',18)->get('users');
```


**LIKE COMBINATION**
--

**like():**
```sh
$result = DB::like('name','Ali')->get('users');
```
```sh
$result = DB::like(array('name' => 'Ali', 'city' => Ist))->get('users');
```

**You can also locate the reference point by sending a third parameter:**
```sh
before:
	$result = DB::like('name', 'Ali','before')->get('users');
	
	print out:
	//users.name LIKE '%Ali'

after:
	$result = DB::like('name', 'Ali','after')->get('users');

	print out:
	//users.name LIKE 'Ali%'
```
<br />
**or_like():**
```sh
$result = DB::like('name','Ali')->or_like('city','Ist')->get('users');
```
<br />
**not_like():**
```sh
$result = DB::not_like('name','Ali')->get('users');
```
<br />
**or_not_like():**
```sh
$result = DB::not_like('name','Ali')->or_not_like('city','Ist')->get('users');
```

**ORDER BY**
--
**order_by():**
```sh
$result = DB::->order_by('name','DESC')->get('users');
```
<br />
**order_by('random'):**
```sh
$result = DB::->order_by('name','random')->get('users');
```


**GROUP BY**
--

**group_by():**
```sh
$result = DB::group_by('name')->get('users');
```

**HAVING**
--
**having():**
```sh
$result = DB::group_by('name')->having("name = 'Ali'")->get('users');
```

<br />
**or_having():**
```sh
$result = DB::group_by('name')
	->having("name = 'Ali'")->or_having('age',18)->get('users');
```

**LIMIT**
--
**limit():**
```sh
$result = DB::limit(1)->get('users');
```

instead of the **offset** method is also useful for:
```sh
$result = DB::limit(2,1)->get('users');
```

**OFFSET (skip data)**
--
**offset():**
```sh
$result = DB::offset(5)->get('users');
```

**JOIN TABLES**
--


As simple as possible to join tables.

First example:
```sh
DB::select('t1.name, t2.city')
	->from(DB::dbprefix('users') . ' t1')
	->join(DB::dbprefix('cities') . ' t2',"t2.id = t1.city_id",'inner')
	->where('t1.age >',18)
	->get();
```
We combine the member table where the city table. And we have defined the coming of the age of 18 and where the.
> **Note:**
> We have sent the left marked as the third parameter in the join method.
> Parameters that are available here:
> 
 - **inner** (INNER JOIN)
 - **left** (LEFT JOIN)
 - **right** (RIGHT JOIN)
 - **left outer join** (LEFT OUTER JOIN)
 - **right outer join** (RIGHT OUTER JOIN)
 - **cross** (CROSS JOIN)

**inner** parameters will work as default.

Let's make different example:
```sh
DB::select('t1.name, t2.city')
	->from(DB::dbprefix('users') . ' t1')
	->join(DB::dbprefix('cities') . ' t2',"t2.id = t1.city_id",'inner')
	->join(DB::dbprefix('countries') . ' t3','t3.id = t2.country_id','left')
	->where('t1.age <',30)
	->where('t1.age >',18)
	->get();
```
**INSERT**
--
There are several ways to add data to the table.

**First:**
```sh
DB::insert('users',array(
		'name' => 'Ali',
		'city' => 'Istanbul',
		'age' => 21
	)
)
```
<br />
**Another use:**
```sh
DB::set('name','Ali');
DB::set('city','Istanbul');
DB::set('age','18');
DB::insert('users');
```
<br >
**and another use than:**
```sh
class User {
	public $name = 'Ali';
	public $city = 'Istanbul';
	public $age = 18;
}

DB::insert('users', new User());
```