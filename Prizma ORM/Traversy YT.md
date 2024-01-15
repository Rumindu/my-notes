* First create node module using `npm init`
* Install type script as dev dependencies `npm i typescript ts-node @types/node -D`
* Creating TSX config file `npx tsc --init`
* Installing prisma `npm i prisma`
* Start prisma `npx prisma init --datasource-provider mysql`
\* Here `mysql` is data source provider name if it is PostgreSQL it should change as `postgresql`.
* After execute this command we can see *.env* file. Here we need to add our db name.
```.env
DATABASE_URL="mysql://root@localhost:3306/todo"
```
* For more credential details according to the db provider visit  [Connection URLs](https://pris.ly/d/connection-strings)
* **Prisma -> schema.prisma** file we model or create our tables.
	```bash
	├ Prisma
	|	├ schema.prisma
```

## Creating tables
```bash
model task{

  id        Int      @id @default(autoincrement())

  details     String

  completed Boolean  @default(false)

}
```
 * migrating prisma schema `npx prisma migrate dev --name init`


