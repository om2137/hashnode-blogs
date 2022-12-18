# Authentication/login system with JWT and NextAuth
protected routes in Next.js

# Overview

User login/authentication is the main feature of any web application. There are various types of frameworks to authenticate users like auth0 and NextAuth. In this article, we will see hands-on, how to authenticate users. Also, we will implement protected routes with middleware provided by next.js so that users cannot directly access the website with URLs/links.

## The stack used in this project is as follows:

*   NextJS
    
*   TailwindCSS
    
*   Typescript
    
*   MongoDB
    

# Implementing User authentication/login system in Next.js

### Step 1:

Create ‘auth’ folder in ‘Pages’ and in it create signin.tsx. This will be used as the front end (SignIn form) to take the input from the user trying to signin.

```typescript
//code for signin.tsx
import React, { useState } from "react";
import Box from "@mui/material/Box";
import Router from 'next/router'
import Button from '../../components/Button';
import { signIn } from "next-auth/react";

export default function login() {
  
  const [username, setUsername] = useState<string>("");
  const [password, setPassword] = useState<string>("");
  const [message, setMessage] = useState<string>("LogIn");
  
  const handleSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault();
    const res = await signIn("credentials", {
      username: username,
      password: password,
      redirect: false,
      body: JSON.stringify({ username, password }),
    })
    if ( res?.status === 200) {
      Router.replace("/");
    }else{
      setMessage("Invalid username or password");
    }
  };



  const style = {
    position: "absolute" as "absolute",
    top: "50%",
    left: "50%",
    transform: "translate(-50%, -50%)",
    
    bgcolor: "background.paper",
    border: "1px solid #000000",
    borderRadius: "4px",
    boxShadow: 12,
    pt: 3,
    px: 2,
    pb: 3,
  };
  return (
    <>
      <Box
        sx={{ ...style }}
        className=" md:w-[35rem] md:h-[40rem] flex justify-center my-auto items-center "
      >
        <div className="w-64">
          <h1 className="flex justify-center items-center text-4xl font-semibold ">
            {message}
          </h1>
          <form
            onSubmit={handleSubmit}
            method="POST"
            action="/api/login"
            className="flex flex-col p-10"
          >
            <input
              type="text"
              name="username"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
              className=" border border-black rounded-lg p-2 text-lg"
            />
            <br />
            <input
              type="password"
              name="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              className=" border border-black rounded-lg p-2"
            />
            <br />

            <Button label="login" type="submit" className="flex justify-center items-center bg-blue-500 hover:bg-blue-400 px-3"/>
            <br />
          </form>
        </div>
        
      </Box>
    </>
  );
}
```

### Step 2:

nextAuth: link Install NextAuth in your project with the following command :

> npm i next-auth

### Step 3:

After installation create an ‘auth’ folder in ‘pages/api’ in your project, in that auth folder create “\[...nextauth\].ts. In the above code \[...nextauth\].ts file we use a JWT session and tokens for user authentication for ongoing sessions. We use the credentials provider to provide and verify the credentials, the logic of taking in credentials and verifying it is done here. After verifying the credentials desired output is returned.

Username and Password are the credentials taken as credentials and verified with the stored environment variables and verified in \[...nextauth\].ts

```typescript
//code for nextauth.ts
import { NextAuthOptions } from "next-auth";
import NextAuth from "next-auth/next";
import CredentialsProvider from "next-auth/providers/credentials";

const user = process.env.USER; 
const pass = process.env.PASS;

const authOptions: NextAuthOptions ={
    session:{
        strategy: 'jwt',
        maxAge: 60*60*24,//valid till 1 day
    },
    providers: [
        CredentialsProvider({
            type: 'credentials',
            credentials:{},
            authorize(credentials, req){
                const { username, password } = credentials as { username: string, password: string };
                if(username !== user || password !== pass ){
                    throw new Error("Login Failed"+username+" "+password);
                };
                return {
                    id: 'admin', 
                    name: 'yourname',
                    role: 'admin',
                };
            }
        })

    ],
    pages: {
        signIn : '../../auth/login',
    },
    callbacks: {
        jwt(params) {
            if(params.user?.role){
                params.token.role = params.user.role;
            }
            return params.token;
        },
        
    }
}

export default NextAuth(authOptions);
```

### Step 4:

Now to test signin page we will create a signin button on the index page which will take us to signin page. later while implementing protected routes we will directly land on login page if the JWT tokens are expired or not present i.e a user is not verified. // code for index signin() function

## Behavior:

![workflow](https://cdn.hashnode.com/res/hashnode/image/upload/v1671374140284/5HoPlVk6A.png align="center")

# Implementing protected routes

### Step 1:

Create a middleware.ts file in the root directory.

```typescript
import { withAuth } from "next-auth/middleware"
import { NextResponse } from "next/server"

export default withAuth(
  function middleware(req) {
    return NextResponse.rewrite(req.url)
  },
  {
    callbacks: {
      authorized: ({ token }) => token?.role === "admin",
    },
  }
)

export const config = { matcher: ["/","/yourroutes","/moreroutes"] }
```

middleware.ts code

### Step 2:

Put NEXTAUTH\_SECRET(Environment Variable) in the .env file.

### Step 3:

Now put the routes you want to protect in the middleware

```typescript
export const config = { matcher: ["/","/yourroutes","/moreroutes"] }
```

# End Credit:

In this short article, we have seen how to implement authentication in React with NextAuth and JWT token. Also implemented Protected routes using middleware.