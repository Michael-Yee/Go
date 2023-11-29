# Boilerplate

The following code set up basic scaffolding for a simple CRUD server.  

Start server:

```bash
go build -o out && ./boilerpalte
```

---

The following tasks was performed in creating this project:

## 1. Create a new module

* Create a new Go module with `go mod init`.
* Add module requirements and sums:
```bash
go mod tidy
```

## 2. Install packages

Install the required packages using `go get`:

* [chi](https://github.com/go-chi/chi/v5)
* [cors]https://github.com/go-chi/cors
* [godotenv](github.com/joho/godotenv)

## 3. Env

The `.env` file will be used to to store environment (configuration) variables.

* [godotenv.Load()](https://pkg.go.dev/github.com/joho/godotenv#Load) to load the variables from the file into your environment.
* [os.Getenv()](https://pkg.go.dev/os#Getenv) to get the values.

## 4. Router and server

1. [chi.NewRouter](https://pkg.go.dev/github.com/go-chi/chi/v5#NewRouter)
2. [router.Use](https://pkg.go.dev/github.com/go-chi/chi#Router.Use) to add the built-in [cors.Handler](https://pkg.go.dev/github.com/go-chi/cors#Handler) middleware.
3. We created a sub-router for the `/v1` namespace and mounted it to the main router.
4. [http.Server](https://pkg.go.dev/net/http#Server) and add the port and the main router to it.
5. Start the server using `ListenAndServe()`.

## 5. JSON helper functions

* `respondWithJSON(w http.ResponseWriter, status int, payload interface{})`
* `respondWithError(w http.ResponseWriter, code int, msg string)` (which calls `respondWithJSON` with error-specific values)

The above helper functions write an HTTP response with:

* A status code
* An `application/json` content type
* A JSON body

## 6. Health handler

Health handler for `GET /v1/health` requests. It will return a 200 status code and a JSON body:

```json
{
  "status": "ok"
}
```

## 7. Error handler

Error handler for `GET /v1/error` requests. It will return a 500 status code and a JSON body:

```json
{
  "error": "Internal Server Error"
}
```
