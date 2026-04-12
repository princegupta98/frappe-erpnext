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
