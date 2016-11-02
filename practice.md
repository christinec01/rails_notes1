in link_to, add remote: true to "prevent default behavior"

in stuffs_controller
```
  def new
    @stuff = Stuff.new
    if request.xhr?
      render partial: 'form', locals {@stuff: stuff}
    end
  end
  ```
  
  in main.js
  ```
  $(document).on("turbolinks:load", function(){

  $("#new-stuff-path").on('ajax:success', function(event, response){
    console.log("hiya");
  })
});
```
the on('ajax:success', function(event, response){
    console.log("hiya"); 
    is just the syntax that you use, once this works, replace console log with:
    ```
        $("#results-div").append(response)
    $("#new_stuff_path").toggle();
    ```
   
   next, to prevent the form from routing to a new page, 
   in the _form.html.erb file:
   ```
   <%= form_for(stuff remote: true) do |f| %>
   ```
   
   AJAX (OLDSCHOOL)
   ```
     $('#results-div').on("submit", "form", function(event){
    event.preventDefault();
    console.log("PREVENTED");

    console.log(this);
    // console.log();
    $.ajax({
      url: '/stuffs.json',
      method: 'post',
      data: $(this).serialize()
    }).done(function(response, status){
      console.log('response', response)
      console.log('status', status)
    })
  })
});
```

```
   AJAX (RAILS-WAY)
$(document).on("turbolinks:load", function(){

  $("#new-stuff-path").on('ajax:success', function(event, response) {
    $("#new_stuff_path").toggle();
    $("#results-div").append(response)
  })
  
  ```
  
