.. Citadel Server documentation master file, created by
   sphinx-quickstart on Tue Jan 26 12:38:25 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Citadel Server Documentation
==========================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:


This server acts as the center of the entire Citadel stack. It coordinates the communication between the client,
database, and all associated data and model microservices. Key features include a robust API, authentication and
permissions, and a layer of abstraction between the actual training/prediction and the user.


Core Modules
==========================================

Main
---------------------------------------------------------

The main file handles the startup/shutdown of the server and is the file directly associated with
FastAPI. CORS requests and router registration is handled via this file.

.. automodule:: main
   :members:

.. note:: The main.py file is only used for startup/shutdown and registering routers. No actual
   computation or logic takes place in this file.


Dependency Server File
---------------------------------------------------------

This file contains all of the shared objects used throughout the server. Ranging from Pydantic models to
constants, it is the single location for objects that are used between modules or passed around frequently.

.. automodule:: dependency
   :members:


Database Connection File
---------------------------------------------------------

This is the only file in the server that will make direct PyMongo calls to the server's MongoDB instance. The
collections referenced in here and the methods will execute pre-defined queries based on the various HTTP
requests received by the server. No query is ever directly exposed to an endpoint or is directly accessible
by a client.

.. automodule:: db_connection
   :members:

HTTP Routers
==========================================

Model Prediction Router
---------------------------------------------------------

The model prediction router handles the connection between the server and model microservices. This allows
for users to create training requests and view training results. Also, support for model registration and
utilities are included in this file

.. automodule:: routers.model
   :members:

Dataset and Training Router
---------------------------------------------------------

The dataset and training router handles the connection and requests between the server and registered datasets.
This includes the initial dataset registration, creating training requests, viewing training result statistics,
and downloading trained model files.

.. automodule:: routers.training
   :members:


Authentication Router
---------------------------------------------------------

Authentication on the server is handled via API keys and OAuth2 Bearer Tokens. Almost all endpoints which interact
with authentication and API keys are stored in this file, as well as the methods which act as helpers for OAuth2
and role validation.

.. automodule:: routers.auth
   :members:

Docker Redis Worker
==========================================

Docker handles the integration of workers which interact with various redis-queues used by the server.
There is almost no worker-specific code other than the worker.py file, as the workers receive a copy of all of
the server files to interact with.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
