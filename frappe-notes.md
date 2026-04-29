# Introduction-

ERPNext is a free and open-source integrated Enterprise Resource Planning software developed by Frappé Technologies Pvt. Ltd. in Frappe Framework

# Frappe Framework Introduction-
Frappe is a full stack, batteries-included, web framework written in Python and Javascript with MariaDB as the database.

It's pretty generic and can be used to build database driven apps.

Meta-data is a first class citizen in Frappe. It is used to generate database tables, design forms and configure a lot of features.

Meta-data is stored in a Model which is known as DocType in Frappe.

It comes with a feature rich admin interface called the Workspace

Frappe comes with User and Role management out of the box.

A User is someone who can login to the system and perform authorized actions like creating, updating or deleting records.

A Role is a mapping of DocTypes and actions allowed to perform on it.

Frappe Framework uses Python for the backend.

The front-end is an SPA built using Javascript (jQuery).

It provides Out Of the box-
	Realtime (NodeJS and socketio)
	Background Jobs (Python RQ) Redis QUeue
	Email (send and receive emails)
	Printing & PDF (Jinja Templates & drag-and-drop Print Format Builder)

# ERPNext Web App Introduction-
ERPNext is a web application and it is developed in Frappe framework.

ERPNext is a full-featured business management solution that helps SMEs(Small/Medium Sized Enterprises) to record all their business transactions in a single system.

It is Stock/Warehouse management system.
It has CRM.
It has HR module.
It has Project mgmt.

ERPNext will help to:
	Track all invoices and payments.
	Know what quantity of which product is available in stock.
	Identify and track your key performance indicators (KPIs).
	Identify open customer queries.
	Manage employee payroll.
	Assign tasks and follow up on them. (PM)
	Maintain a database of all your customers, suppliers, and contacts.
	Prepare quotations. (Sales order/invoices)
	Track your budgets and spending.
	Determine effective selling price based on the actual raw material, machinery and effort cost.
	Get reminders on maintenance schedules.
	Publish your website. (Integrate your own product with ERPNext)

ERPNext modules:
	Accounting
	Asset management
	Customer relationship management (CRM)
	Human resource management (HRM)
	Payroll
	Project management
	Purchasing
	Sales management
	Warehouse management system and more...

# Installation-

Section 1: Install Frappe Bench and its dependencies

Section 2: Initailize New Frappe Bench & Create Site, install ERPNext and hrms apps into site

# Bench

Bench is the command line tool to manage Frappe apps and sites.

It provides an easy interface to help you setup and manage multiple sites and apps based on Frappe Framework.

To initialize a new bench instance (project), run the following command:
bench init <bench_name> <version_name(optional)>
			dir name

General Usage-

Development-

bench start 

bench new site

bench new app

bench app into site

Change from production mode -> developer mode:
	bench set-config developer_mode 1

	Check in site config if dev mode is on:
		cat sites/[site-name]/site_config.json

		now, we can use this becnh for development purpose

Create new-app command:
	bench new-app Demo-App

	enter title, description, publisher, email, mit license

check if app is installed:
	bench version

install created app into the site:
	bench install-app demo_app

check app is installed in webiste by going to about section

# Frappe Bench - Directory Structure

|--Procfile
|--apps
|	|--frappe
|--config
|	|--pids
|	|--redis cache.conf
|	|--redis queue.conf
|	|--redis socketio.conf
|--env
|	|--bin
|	|--include
|	|--lib
|	|--share
|--logs
|	|--backup.log
|	|--bench.log
|--sites
	|--apps.txt
	|--assets
	|--common_site_config.json

apps - installed applications
config - redis, socketio and nginx config files
env - python venv & req libraries for frapppe/erp applications
logs - web log, worker log, bench log and other log for each process
sites - instance/sites of our apps, static asset dir, apps list

# Frappe App - Directory Structure

apps/library_mgmt_app/ 	<- root
	|
	|--MANIFEST
	|--README.md
	|--library_mgmt_app/	<- modules
		|--hooks.py
		|--library_mgmt_app/
			|--init_.py
		|--modules.txt
		|--patches.txt
		|--public/
			|--css/
			|--js/
		|--templates/
			|--__init__.py
			|--includes/
			|--pages/
				|--__init__.py
		|--www/
	|--requirements.txt
	|--setup.py


hooks - extend/intercept standard functionality provided by frappe framework

module - to group diff doctype, dash repor with same func

module.txt- list of module deined inside application

patches.txt - write patches

public/ - static files shared with nginx in production

templates/ -jinija templates used to render webview

www/ - for storing web pages

requiremnets.txt - req for render app 

## ERPNext App Structure 

requirements.txt is no longer needed in apps its managed centrally on bench level

setup.py is replaced by pyproject.toml it is entry point for python packaging

inside app modules
	we can see module list in modules.txt or module folders
	hooks.py has diff hooks available for app

	inside specific app module
		doctype directory- all doctype for this module
		report directory- reports associated with module
		workspace directory-

# Create New Module

IN Website - 
	Home -> Build -> Module Def -> Add New -> Module name, select app -> Save Module

# Create New Doctype

IN Website - 
	Home -> Build -> Doctype -> Add New Doctype-> 
		Enter Doctype name, Select Module
			Add Section
				Add Field
					Enter Field Label
					Enter Field Type
					Enter Field Name (for programming purpose)
						Save

	It will create "new database table"

Go to Doctype list -> Add new Doctype

we can check doctype controlling files in our app module doctype directory
and to see table desc added in mariadb we can

access mariadb:
bench mariadb

access newly created table using tab prefix then doctype name
desc `tabDemo Doctype`;

select * from `tabDemo Doctype`;

exit query results 
	q

exit mariadb console
	ctrl + d

# Doctype | DocField

Add a new Field in doctype and try with differrent Field type(dt)

	Link Field type is used to link to other doctype and should be mentioned in Options in Add Field Form. when filling form linked doctype data will be shown as dropdown list

	Select Field type is used to select bw options and available options should be mentioned in Options each in new line in Add Field Form

	Data Field type - takes string ddata

	Column Break and Section Break are used for styling the form

# Doctype | DocField Properties

Each field has properties
	mandatory
	in list view
	in Standard Filter
	default values of field
	hidden
	read only
	set only once
	condition (display depends on)
	description

# Doctype Naming

Open Doctype Settings (Edit Doctype) ❌
Open Doctype Settings > dot menu > Customize ✅

1. Naming by Field- name in list will be shown based on field name
	field:[fieldname]

	Auto Name: field:prince

	prince

2. Naming by Prompt- name will be entered by user from input field
	Prompt

	Auto Name: Prompt

	entered_name

3. Naming by Series- Series by prefix (separated by a dot)
	PRE.#####
		# represents 0

	Auto Name: PRE.#####

	PRE00001, PRE00002, ...

4. Naming by format: Replace all braced words (fieldnames, date words (DD, MM, YY), series) with their value. Outside braces, any characters can be used.
	format:(MM) morewords(fieldname1)-(fieldname2)-(#####}

	Auto Name: format:TTT-{MM}-{abc}-{####}	
		MM DD YY should be capital

	TTT-04-priince-0001

5. naming_series: By Naming Series (field called naming_series must be present)

	Add field called (From Edit Doctype)
		Label : NSeries
		Name : naming_series
		Type : Select

	Auto Name: naming_series:

	Go to Document Naming Settings: 
		Select Transaction: choose our Doctype from dropdown

		Enter Series List:
			TY-
			RRR-.###
			GHGH-.####

	Add data to our doctype list:
		Select series from NSeries when adding data

# Doctype | Types of DocType

DocType
	Add DocType
		name: Normal DocType
		module: select programming module
		fields: Add 2 fields of type Data

	Add another DocType
		name: Submittable DocType
		module: select programming module
		fields: Add 2 fields of type Data
			check is Submittable

		Now go to doctype list
		add new doc data & save
		then doc is saved and document is in draft state & submit
		then doc is in submitted state and user cant edit, it is in read-only mode

	Add another DocType
		name: Single DocType
		module: select programming module
		fields: Add 2 fields of type Data
			check is Single

		Now for single doctype there is no list because only 1 data is there
		no report generation
		no multiple document submit

	Add another DocType
		name: Tree DocType
		module: select programming module
		fields: Add 2 fields of type Data
			check is Tree

		in tree doctype list switch to tree view

		add child (check group node if child has sub-child) and in this view press edit to add data to node

# Doctype | Child Doctype

	Add New DocType
		name: Child Doc
		module: select programming module
		fields: Add 2 fields of type Data
			check is Child Table

	no child doctype list
	all child doctype belongs to some parent doctype, so we cant create child doctype data individually

	Goto Single Doctype
		Add field 
			Child	- label
			Table	- type
			Child Doc - option

	In Child Doc 
		Enable grid view for all fields

	Single Doctype
		Add data
			in child field we can add row as per child doctype

	Check Table Structure
		bench mariadb
			desc `tabChild Doc`;
			select * from `tabChild Doc`;
			exit;

