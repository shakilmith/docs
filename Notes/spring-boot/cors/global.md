
```
Global CORS configuration: (write it in the application class)
	@Bean
	public WebMvcConfigurer corsConfigurer() {
		return new WebMvcConfigurer() {
			@Override
			public void addCorsMappings(CorsRegistry registry) {
				registry.addMapping("/greeting-javaconfig").allowedOrigins("http://localhost:8080");
			}
		};
	}

Method Level CORS configuration: 
@CrossOrigin(origins = "http://localhost:8080") //add it on the HTTP Get/POST/DELETE request
```