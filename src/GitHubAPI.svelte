<script>
function getUser(name){
 fetch(`https://api.github.com/users/${name}`)
  .then(function(response) {
    return response.json();
  })
  .then(function(json) {
    console.log(json);
  });
};

//get user data
getUser('yourUsernameHere');
</script>