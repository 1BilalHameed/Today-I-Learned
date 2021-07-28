# Passing Header Parameter to Retrofit 2 Two Ways

you can pass header parameter by using `Retrofit 2` by two ways

<ol>
  <li>Static Way</li>
  <li>Dynamic Way</i>
</ol>

## Static Way

The static way mean you have to define header parameter everytime with a new request it is done in the following way

```
Headers("token:tokenvaluehere")
Get("xyz")
fun getAllUsers()
```


## Dynamic Way

The dynamic way mean you do not have to define header every time you can provide one type when request is being build for example

```
    val httpClientHeader = OkHttpClient.Builder()
        httpClientHeader.addInterceptor { chain ->
            val chainReq = chain.request()
            val newRequest = chainReq.newBuilder()
                .addHeader("x-customer-key", "eKhPkRnUrWtYw3y5")
                .addHeader("x-customer-secret", "mSpVsXuZx4z6B9Eb")
                .method(chainReq.method(), chainReq.body())
                .build()
            chain.proceed(newRequest)
        }

        val retrofit =
            Retrofit.Builder()
                .baseUrl("YOUR BASE URL")
                .addConverterFactory(GsonConverterFactory.create())
                .client(httpClientHeader.build()).build().create(KistPayRetailerApi::class.java)
```
