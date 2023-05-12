Use is to shorten the program file by not mapping endpoints there.

```c#
using Carter;

var builder = WebApplication.CreateBuilder(args);  
  
builder.Services.AddCarter();  // add to services
  
var app = builder.Build();  
  
app.MapCarter();  // to got all classes which inherit CarterModule or implement ICarterModule
  
app.Run();
```

The endpoints group class is supposed to inherit CarterModule or implement ICarterModule. The endpoint would look like this:

```c#
public class HelloWordModule : CarterModule  
{  
	public HelloWordModule()  
		: base("/hi")  // to group the routes for this class
	{  
	}  
	  
	public override void AddRoutes(IEndpointRouteBuilder app)  
	{  
		app.MapGet("/", () => "Hello World!"); // same as /hi/
		app.MapGet("/1", () => Results.Ok(1)); // same as /hi/1/
	}  
}
```

As the result there is no need in mapping endpoints in the program class.