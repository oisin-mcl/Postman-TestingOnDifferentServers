# Postman-Testing On Different Servers

This code works as a basic framework that allows us to test our code against different build servers. The use case for this is for companies that use different build servers that require testing. For this collection, I have used 3 different servers; "SandBox", "Test" and "Production". This uses the Postman Environment features to achive and will allow code to be as DRY as possible without the need to duplicate your code or tests across each test server you wish to use. 

For this, I have setup a number of different variables that could be used to allow a user to authenticate to different servers. This is just sample variables, so these need changedd to your values, as many or few as are needed. 

Lets look at the environments:
![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/b3d8dfdf-f035-4405-a81b-3eaecc2196a0)

Here there are 3 environments. Each of these hold the various variables that are used to authenticate to the relevant server. Lets look at one:

![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/550b80b7-7992-4ed9-9ba1-d053569e8eeb)

We can see that there is a "Server" variable, that holds the server name, an API Key that would vary depending on the server you use, and then a cookie name and value. Again, these are just examples, but you could hold URLs here, specific cookie values, URL components or endless other options. Each Environment has the same variable names, but each holds their own relevant values that we will test against.

Now, to begin, we must set the Env we wish to use. This is a UI option located here:

![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/6bc1bb45-9666-464d-8476-8bcdef9f8373)

Once you have set the Env you wish to use, we can run a test. Lets look at the request to see how we can test the server being tested on.

First, we can see that the URL of the request contains a variable:
![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/a11c753b-ae8d-48b5-af1e-23a88e5eb1be)

This will add a URL component to the request based on the current server, adding a "-<servername>" to the request. This will be replaced on running with the name of the server. 

Next, lets look at the Headers tab:
![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/2e2ac6ce-438f-4303-9993-4c0ef9046186)

Here, we set 2 dynamic headers. The first is the apikey, and the second is cookie. In real world use cases, both would not be needed as headers to authenticate, but any cookie you wish to set can be done this way, or programatically as shown in my other repos.

The apikey header is set to the value of the Env variable, as are the cookie header details.

With all these dynamic server values set, lets look at how we can test that these are all set correct for each request. For this, I had added the tests to the Collection level, to allow every request we send within this Collection to be checked. 

![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/9c73a9a9-65a1-4bc1-b23e-cba26efc69ad)
Above, we test that the apikey header we set, has indeed been set to what we wish it to be. This can amended to test against preset test data if you wish.

![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/44e01703-0fe8-4db1-8c2e-4cd796854571)
And we can also check that the Server URL component has been set correctly in the "args" of the response.

![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/2d08e030-4d4a-4f2b-b1d8-1308419dc617)
And that the URL component is set in other locations too.

And how does this look on run? Lets see:
![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/9215cae3-d779-49c1-871f-932f41c850a1)

As we can see highlighted, the values are set based on the Env we use, and if we switch to Test, it updates:
![image](https://github.com/oisin-mcl/Postman-TestingOnDifferentServers/assets/56615317/725a64ca-184e-4685-abe3-94bb3aab7dd0)

This is just one basic way of dividing and grouping tests to achieve polymorphism with our requets, to allow us to pass in differing values, to test the same requests using different authentication methods.
