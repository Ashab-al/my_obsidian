rails g graphql:object Post title:String body:Text author:references

rails g graphql:object Author name:String post:has_many