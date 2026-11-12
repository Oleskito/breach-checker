1. Testy z .lower()
cachedir: .pytest_cache
rootdir: /app
collected 8 items                                                                                                                                                                                                   

tests/test_check.py::test_leaked_hash_is_found PASSED                                                                                                                                                         [ 12%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                                                                                                                                    [ 25%]
tests/test_check.py::test_missing_hash_field PASSED                                                                                                                                                           [ 37%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                                                                                                                               [ 50%]
tests/test_check.py::test_uppercase_hash_is_found PASSED                                                                                                                                                      [ 62%]
tests/test_check.py::test_hash_wrong_length PASSED                                                                                                                                                            [ 75%]
tests/test_check.py::test_hash_non_hex PASSED                                                                                                                                                                 [ 87%]
tests/test_check.py::test_hash_not_json PASSED   

2. Testy bez .lower()

tests/test_check.py::test_leaked_hash_is_found PASSED                                                                                                                                                         [ 12%]
tests/test_check.py::test_unknown_hash_is_not_found PASSED                                                                                                                                                    [ 25%]
tests/test_check.py::test_missing_hash_field PASSED                                                                                                                                                           [ 37%]
tests/test_check.py::test_plaintext_password_is_rejected PASSED                                                                                                                                               [ 50%]
tests/test_check.py::test_uppercase_hash_is_found FAILED                                                                                                                                                      [ 62%]
tests/test_check.py::test_hash_wrong_length PASSED                                                                                                                                                            [ 75%]
tests/test_check.py::test_hash_non_hex PASSED                                                                                                                                                                 [ 87%]
tests/test_check.py::test_hash_not_json PASSED                                                                                                                                                                [100%]

===================================================================================================== FAILURES ======================================================================================================
___________________________________________________________________________________________ test_uppercase_hash_is_found ____________________________________________________________________________________________

client = <FlaskClient <Flask 'app'>>

    def test_uppercase_hash_is_found(client):
        response = client.post("/check", json = {"hash": ("a"*40).upper()})
>       assert response.status_code == 200
E       assert 400 == 200
E        +  where 400 = <WrapperTestResponse streamed [400 BAD REQUEST]>.status_code

tests/test_check.py:27: AssertionError
============================================================================================== short test summary info ==============================================================================================
FAILED tests/test_check.py::test_uppercase_hash_is_found - assert 400 == 200
============================================================================================ 1 failed, 7 passed in 0.46s =

## Testy z zajęć nie wykrył usunięcia .lower() z tego względu że podawany hash do testów był w małych literach więc zgadzał się z hashem umieszczonym w pliku z hashami. Po utworzeniu testsu .upper() hash jest podawany w wielkich literach więc usunięcie .lower() powoduje że hash badany nie zgadza się z tym z pliku z hashami.

3. Wynik curl 
HTTP 500

4. Wynik ps-a oraz inspect
NAME                           IMAGE                                                                     COMMAND                  SERVICE    CREATED          STATUS                     PORTS
wirtualizacja_lab-backend-1    wirtualizacja_lab-backend                                                 "flask --app app run…"   backend    14 minutes ago   Exited (1) 7 seconds ago   
wirtualizacja_lab-db-1         postgres:16-alpine                                                        "docker-entrypoint.s…"   db         7 days ago       Exited (0) 7 minutes ago   
wirtualizacja_lab-frontend-1   sha256:72bbaa1e038e17d21c68f8e1d29b530c4d3b2b18d89a9ff460dce327019cfd91   "/docker-entrypoint.…"   frontend   7 days ago       Up 14 minutes              0.0.0.0:8080->80/tcp, [::]:8080->80/tcp
exited 1

# Plik blad.html zawiera stronę kodu błędu 502 - serwer działa poprawnie ale nie otrzymał poprawnej odpowiedzi od bazy danych. ujawnia ona dokładną wersje i numer serwera proxy co na etapie produkcyjnym może pozwolić atakującemu zebrać informacje

5. Wynik docker stats
ID   NAME                           CPU %     MEM USAGE / LIMIT     MEM %     NET I/O           BLOCK I/O       PIDS
eaab1c754a46   wirtualizacja_lab-frontend-1   0.00%     8.031MiB / 3.701GiB   0.21%     22.4kB / 20.9kB   3.6MB / 4.1kB   9

6. Wynik docker compose logs backend
backend-1  |  * Serving Flask app 'app'
backend-1  |  * Debug mode: on                                                                
backend-1  | WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
backend-1  |  * Running on all addresses (0.0.0.0)
backend-1  |  * Running on http://127.0.0.1:5000
backend-1  |  * Running on http://172.19.0.3:5000
backend-1  | Press CTRL+C to quit
backend-1  |  * Restarting with stat
backend-1  | W bazie jest 90 hashy
backend-1  |  * Debugger is active!
backend-1  |  * Debugger PIN: 117-986-214
backend-1  |  * Detected change in '/app/app.py', reloading
backend-1  |  * Restarting with stat
backend-1  | W bazie jest 90 hashy
backend-1  |  * Debugger is active!
backend-1  |  * Debugger PIN: 117-986-214
backend-1  |  * Detected change in '/app/tests/test_check.py', reloading
backend-1  |  * Restarting with stat
backend-1  | W bazie jest 90 hashy
backend-1  |  * Debugger is active!
backend-1  |  * Debugger PIN: 117-986-214
backend-1  |  * Detected change in '/app/app.py', reloading
backend-1  |  * Restarting with stat
backend-1  | W bazie jest 90 hashy
backend-1  |  * Debugger is active!
backend-1  |  * Debugger PIN: 117-986-214
backend-1  |  * Detected change in '/app/app.py', reloading
backend-1  |  * Restarting with stat
backend-1  | W bazie jest 90 hashy
backend-1  |  * Debugger is active!
backend-1  |  * Debugger PIN: 117-986-214
backend-1  | check: hash=7c4a8...
backend-1  | 172.19.0.4 - - [12/Nov/2026 10:59:22] "POST /check HTTP/1.1" 500 -
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1536, in __call__
backend-1  |     return self.wsgi_app(environ, start_response)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1514, in wsgi_app
backend-1  |     response = self.handle_exception(e)
backend-1  |                ^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 1511, in wsgi_app
backend-1  |     response = self.full_dispatch_request()
backend-1  |                ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 919, in full_dispatch_request
backend-1  |     rv = self.handle_user_exception(e)
backend-1  |          ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 917, in full_dispatch_request
backend-1  |     rv = self.dispatch_request()
backend-1  |          ^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/app.py", line 902, in dispatch_request
backend-1  |     return self.ensure_sync(self.view_functions[rule.endpoint])(**view_args)  # type: ignore[no-any-return]
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/app/app.py", line 39, in check
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/bin/flask", line 8, in <module>
backend-1  |     sys.exit(main())
backend-1  |              ^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 1131, in main
backend-1  |     cli.main()
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1560, in main
backend-1  |     rv = self.invoke(ctx)
backend-1  |          ^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 2054, in invoke
backend-1  |     return _process_result(sub_ctx.command.invoke(sub_ctx))
backend-1  |                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1414, in invoke
backend-1  |     return ctx.invoke(self.callback, **ctx.params)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/decorators.py", line 93, in new_func
backend-1  |     return ctx.invoke(f, obj, *args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 979, in run_command
backend-1  |     raise e from None
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 963, in run_command
backend-1  |     app: WSGIApplication = info.load_app()  # pyright: ignore
backend-1  |                            ^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 349, in load_app
backend-1  |     app = locate_app(import_name, name)
backend-1  |           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 245, in locate_app
backend-1  |     __import__(module_name)
backend-1  |   File "/app/app.py", line 19, in <module>
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/bin/flask", line 8, in <module>
backend-1  |     sys.exit(main())
backend-1  |              ^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 1131, in main
backend-1  |     cli.main()
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1560, in main
backend-1  |     rv = self.invoke(ctx)
backend-1  |          ^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 2054, in invoke
backend-1  |     return _process_result(sub_ctx.command.invoke(sub_ctx))
backend-1  |                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1414, in invoke
backend-1  |     return ctx.invoke(self.callback, **ctx.params)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/decorators.py", line 93, in new_func
backend-1  |     return ctx.invoke(f, obj, *args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 979, in run_command
backend-1  |     raise e from None
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 963, in run_command
backend-1  |     app: WSGIApplication = info.load_app()  # pyright: ignore
backend-1  |                            ^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 349, in load_app
backend-1  |     app = locate_app(import_name, name)
backend-1  |           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 245, in locate_app
backend-1  |     __import__(module_name)
backend-1  |   File "/app/app.py", line 19, in <module>
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/bin/flask", line 8, in <module>
backend-1  |     sys.exit(main())
backend-1  |              ^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 1131, in main
backend-1  |     cli.main()
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1560, in main
backend-1  |     rv = self.invoke(ctx)
backend-1  |          ^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 2054, in invoke
backend-1  |     return _process_result(sub_ctx.command.invoke(sub_ctx))
backend-1  |                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1414, in invoke
backend-1  |     return ctx.invoke(self.callback, **ctx.params)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/decorators.py", line 93, in new_func
backend-1  |     return ctx.invoke(f, obj, *args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 979, in run_command
backend-1  |     raise e from None
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 963, in run_command
backend-1  |     app: WSGIApplication = info.load_app()  # pyright: ignore
backend-1  |                            ^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 349, in load_app
backend-1  |     app = locate_app(import_name, name)
backend-1  |           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 245, in locate_app
backend-1  |     __import__(module_name)
backend-1  |   File "/app/app.py", line 19, in <module>
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/bin/flask", line 8, in <module>
backend-1  |     sys.exit(main())
backend-1  |              ^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 1131, in main
backend-1  |     cli.main()
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1560, in main
backend-1  |     rv = self.invoke(ctx)
backend-1  |          ^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 2054, in invoke
backend-1  |     return _process_result(sub_ctx.command.invoke(sub_ctx))
backend-1  |                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1414, in invoke
backend-1  |     return ctx.invoke(self.callback, **ctx.params)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/decorators.py", line 93, in new_func
backend-1  |     return ctx.invoke(f, obj, *args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 979, in run_command
backend-1  |     raise e from None
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 963, in run_command
backend-1  |     app: WSGIApplication = info.load_app()  # pyright: ignore
backend-1  |                            ^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 349, in load_app
backend-1  |     app = locate_app(import_name, name)
backend-1  |           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 245, in locate_app
backend-1  |     __import__(module_name)
backend-1  |   File "/app/app.py", line 19, in <module>
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 
backend-1  | Traceback (most recent call last):
backend-1  |   File "/usr/local/bin/flask", line 8, in <module>
backend-1  |     sys.exit(main())
backend-1  |              ^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 1131, in main
backend-1  |     cli.main()
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1560, in main
backend-1  |     rv = self.invoke(ctx)
backend-1  |          ^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 2054, in invoke
backend-1  |     return _process_result(sub_ctx.command.invoke(sub_ctx))
backend-1  |                            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 1414, in invoke
backend-1  |     return ctx.invoke(self.callback, **ctx.params)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/decorators.py", line 93, in new_func
backend-1  |     return ctx.invoke(f, obj, *args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/click/core.py", line 911, in invoke
backend-1  |     return callback(*args, **kwargs)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 979, in run_command
backend-1  |     raise e from None
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 963, in run_command
backend-1  |     app: WSGIApplication = info.load_app()  # pyright: ignore
backend-1  |                            ^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 349, in load_app
backend-1  |     app = locate_app(import_name, name)
backend-1  |           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/flask/cli.py", line 245, in locate_app
backend-1  |     __import__(module_name)
backend-1  |   File "/app/app.py", line 19, in <module>
backend-1  |     conn = connect()
backend-1  |            ^^^^^^^^^
backend-1  |   File "/app/app.py", line 11, in connect
backend-1  |     return psycopg2.connect(
backend-1  |            ^^^^^^^^^^^^^^^^^
backend-1  |   File "/usr/local/lib/python3.12/site-packages/psycopg2/__init__.py", line 122, in connect
backend-1  |     conn = _connect(dsn, connection_factory=connection_factory, **kwasync)
backend-1  |            ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
backend-1  | psycopg2.OperationalError: could not translate host name "db" to address: No address associated with hostname
backend-1  | 


7. Wynik curl przed poprawką override

StatusCode        : 200
StatusDescription : OK
Content           : {115, 101, 114, 118...}
RawContent        : HTTP/1.1 200 OK
                    Connection: keep-alive
                    Accept-Ranges: bytes
                    Content-Length: 326
                    Content-Type: application/octet-stream
                    Date: Thu, 12 Nov 2026 11:23:25 GMT
                    ETag: "6ae35a13-146"
                    Last-Modified: Th...
Headers           : {[Connection, keep-alive], [Accept-Ranges, bytes], [Content-Length, 326], [Content-Type, application/octet-stream]...}
RawContentLength  : 326

8. wynik curl po poprawce override
HTTP/1.1 404 Not Found
Server: nginx/1.31.8
Date: Thu, 12 Nov 2026 11:27:44 GMT
Content-Type: text/html
Content-Length: 153
Connection: keep-alive

# W trybie produkcyjnym nie jest tworzony wolumen na dysku (plik overridde z bind-mount nie jest uzywany) tylko pliki index,script,style są kopiowane za pomocą instrukcji copy w pliku dokcerfile (czyli umieszczane są tylko te pliki w kontenerze)