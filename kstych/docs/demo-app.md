Now that you have understood the basics of the Kstych framework, how about we build a simple demo application.

<font color='#7540EE'>

[Blog Application in Kstych framework](#blog-application-in-kstych-framework)


</font>
- - - -

# Blog Application in Kstych framework

Let's create a simple blog application using the Kstych framework

### Setup the Kstych framework

1. In your home directory, start by creating a new directory named `BlogPost` and change to that directory.

        mkdir BlogPost && cd BlogPost

1. Clone the Kstych framework.

        git clone https://github.com/kstych/framework

1. Switch to the superuser and change to the `framework` directory.

        sudo su
        cd framework

1. Run the Kstych framework. Open your browser and type `http://localhost` in the browser search bar. You would be prompted with the **LoginID** and **Password**. Log in using `admin` and `yb9738z` as the default credentials.

        ./kstych.sh

### Create the BlogPost Module and Model

Go to the **Designer** page and click **Modules**. Create a new Module named `BlogPost` and a Model named `Post`. You can choose a different Module and Model name of your choice. Click **Save Settings**.

<img src="../images/demo_application_images/create_module.png" />

### Provide access to the Module

Once you have the Module created, you need to provide access to the Module. To do this:

1. Go to **Admin**-> **Role**.
1. Double-click the role for which you want to add the module.
1. Click **Create New** to add the module (in this example, `BlogPost`) and select **Write** permission in the **ACL** drop-down.
1. Click **Save RoleModule** and click **Save Role**.

    <img src="../images/demo_application_images/add_role.png" />

### Adding columns to the Model

1. Go to the **Designer** page and click **Models**.
1. Select the Modules and Models from the drop-down. (In this example, `BlogPost` and `Post`)
1. Enter the table name (In this example, `posts` is the table name).
1. In the *Schema* table, enter the required columns (`intro`, `title`, `body`, `user_id`) as shown below. You can add more columns as required.

    <img src="../images/demo_application_images/columns.png" />

### Create Controller, Assets, and Views for the application

#### Create Controller

1. In the **Designer** page and click **Custom**.
1. Locate the **packages** directory and create a new directory with the same name as the Module Name (in this example, it is `BlogPost`).
1. In the **BlogPost** directory, create another directory named **Controller**.
1. In the **Controller** directory, create your controller file; in this example, it is `BlogPost.php`. Add the contents of the example code below and save the file.

    <img src="../images/demo_application_images/create_directory.png" />


Following is an example directory structure for creating Controllers within the **packages** directory.

<img src="../images/demo_application_images/sample_dir_str.png" width="250" height="200" />

Following is the sample `BlogPost.php` controller code that uses the basic resource controllers and is customized with SQL queries to do perform the CRUD operations-insert, delete and update in the `posts` table.

**Contoller:** `/custom/ext/packages/BlogPost/Controller/BlogPost.php`

```
<?php namespace App\Custom\BlogPost\Controller;

use DB;
use Auth;
use Request;
class BlogPost
{
    public function __construct(){}

    public function index()
    {
      $posts = kmodel('Post')::latest()->paginate(15);
      return view("custom.blogpost.index",['posts'=>$posts]);
    }
    public function show($id)
    {
      $post = kmodel('Post')::find($id);
      $latests = kmodel('Post')::latest()->where('id','!=',$id)->take(3)->get();

      return view("custom.blogpost.show",['post'=>$post,'latests'=>$latests]);
    }
    public function create()
    {
        $id = request('id');
        $post = kmodel('Post')::find($id);
        if(!$post) $post = kmodel('Post')::make();
        return view("custom.blogpost.create",['post'=>$post]);
    }
    public function store()
    {
      request()->validate([
    		'title'=>'required',
    		'intro'=>'required',
    		'body'=>'required',
    	]);

      $Post = kmodel('Post');

    	$post = new $Post();
    	$post->title=request('title');
    	$post->intro=request('intro');
    	$post->body=request('body');
    	$post->user_id=Auth::user()->id;
    	$post->save();

      return redirect('/blogpost');
    }
    public function edit($id)
    {

    }
    public function update($id)
    {
    	$Post = kmodel('Post')::find($id);
    	$Post->title = request('title');
    	$Post->intro = request('intro');
    	$Post->body  = request('body');
    	 $Post->save();

      return redirect('/blogpost/'.$id.'?'.request('title'));

    }

    public function destroy($id)
    {
      $obj = Kmodel('Post')::where('id',$id)->first();
      if($obj) $obj->delete();
   	  return redirect('/blogpost');

    }
}

```

In the above code snippet, following are the methods used:

- `index()` to show our homepage.
- `show()` to display the posts.
- `store()` to insert data in `posts` table.
- `update()` to update the data in `posts` table.
- `destroy()` to delete the data from `posts` table.

#### Create Assets

**assets** directory is used to store images, `.css`, and `.js` files. To add files into the **assets** directory:

1. In the **Designer** page and click **Custom**.
1. Locate the **assets** directory and create a new directory with the same name as your Module name, but in *small case* (in this example, it is `blogpost`).

    <img src="../images/demo_application_images/assets.png" />

    For example, if you have a `xyz.css` file in the `assets`/`css` directory, then your URL for this example would look like: `custom/blogpost/css/xyz.css`

#### Create Views

In the **views** folder, you store all the template files required for your application. To add templates into the **views** directory:

1. In the **Designer** page and click **Custom**.
1. Locate the **views** directory and create a new directory with the same name as your Module name, but in *small case* (in this example, it is `blogpost`). Within the **blog post** directory, you can add all your application template files.

    <img src="../images/demo_application_images/views.png" />

1. In this example, let's create a file name `template.blade.php` or any suitable file name. Add the below content and save the file.

    **Template file:** `/custom/ext/views/blogpost/template.blade.php`

        <!DOCTYPE html>

        <html lang="en">
        <head>
            <meta charset="utf-8">
            <meta http-equiv="X-UA-Compatible" content="IE=edge">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <title>AwesomeBlogs</title>

            <!-- Here we will link css file-->
            <link rel="stylesheet" href="{{ url('custom/blogpost/css/main.css') }}">
            <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

            <style>
                body{font-size:25px;}
                h3{font-size:40px;}
            </style>
        </head>
        <body>
            <div id="header">
            <div class="container" style="max-width:90%">
                <a href="/blogpost" style="font-size:35px;padding:0px;float:left;">Awesome Blogs</a>
                <ul id="header-nav">
                <li><a href="/blogpost/create">CreatePost</a></li>
                </ul>
            </div>
            </div>

            @yield('content')

        <!-- Footer -->
        <footer class="page-footer font-small" style="background-color:#1ABC9C;">

        <!-- Copyright -->
        <div class="text-center py-3">
            <a href="/localhost/blogpost" style="color:white"> AwesomeBlogs - Kstych</a>
        </div>
        <!-- Copyright -->

        </footer>
        <!-- Footer -->


        </body>
        </html>

1. Now, let's create template files to display our blog posts. Create an index template file-`index.blade.php` (it is suggested to use the same file name to use the default routes).

    <img src="../markups/default-route.svg">

    **Template file to display blog post:** `/custom/ext/views/blogpost/index.blade.php`

        @extends('custom.blogpost.template')

        @section('content')
            <div id="content" style="max-width:1000px;margin:10px auto">

            @forelse($posts as $post)

                <div class="post-container">
                <div class="post" style="padding:20px 30px;">
                <h3 class="post-title"><a href="/blogpost/{{$post->id}}?{{$post->title}}">{{$post->title}}</a></h3>
                <div class="post-content">
                    <p>{{$post->intro}}</p>
                </div>
                <div class="post-author">
                    <img src="{{$post->user->getFileLink('photo')}}" alt="user profile pic">
                    <span>{{$post->user->fullname??''}}</span>

                </div>
                </div>
            </div>

                @empty
                <div class="post-container">
                    <div class="post" style="text-align: center;">
                    Nothing here yet
                    </div>
                </div>
            @endforelse


            </div>
        @endsection

    If you go to `localhost/BlogPost` in your browser, you should see an output similar to the following:

    <img src="../images/demo_application_images/blog-output-1.png" />

1. Now, let's add another template file- `create.blade.php` for creating a blog post.

    **Template file to create a blog post:** `/custom/ext/views/blogpost/create.blade.php`

        @extends('custom.blogpost.template')

        @section('content')

            <div class="container" style="margin-bottom:20px;">
                <br/>
                    <h3>Create New Post</h3>
                <br/>
                <form @if($post->id) action="/blogpost/{{$post->id}}" @else  action="/blogpost" @endif method="POST"  >
                    @csrf
            @if($post->id) <input name="_method" type="hidden" value="put">@endif
                <div class="form-group">
                    <label>Title</label>
                    <input type="text" class="form-control"  value="{{$post->title}}"  name="title" placeholder="Enter title" required>

                </div>
                <div class="form-group">
                    <label>Intro</label>
                    <textarea type="textarea" class="form-control" name="intro"   placeholder="Enter Intro" required>{{$post->intro}}</textarea>
                </div>


                <div class="form-group">
                    <label>Body</label>
                    <textarea type="textarea" class="form-control" name="body"    placeholder="Enter body" required>{{$post->body}}</textarea>
                </div>

                <center>
                    <button type="submit" class="btn btn-primary" >Submit</button>
                </center>
                </form>
            </div>
        @endsection

    If you go to `localhost/blogpost/create` in your browser, you should see an output similar to the following:

    <img src="../images/demo_application_images/blog-output-2.png" />

1. Following is another template file that displays the blog post details -`show.blade.php`

    **Template file to display a blog details page:** `/custom/ext/views/blogpost/show.blade.php`

        @extends('custom.blogpost.template')

        @section('content')

        <div id="content" style="max-width:80%;margin:10px auto;">
            <div class="post-container container " style="padding-bottom:10px;">
                <div class="post" style="padding:20px;">
                <h3 class="post-title"><a href="/blogpost/{{$post->id}}?{{$post->title}}">{{$post->title}}</a></h3>
                <div class="post-content">
                    <p>{{$post->body}}</p>
                </div>
                <div class="post-author">
                    <img src="{{$post->user->getFileLink('photo')}}" alt="user profile pic">
                    <span>{{$post->user->fullname}}</span>
                </div>
                </div>
                <div class="container">
                    <div class="row">
                    <div class="col-sm-6" style="text-align:right">
                        <form method="Post" action="/blogpost/{{$post->id}}" >
                            @csrf
                            <input name="_method" type="hidden" value="DELETE">
                            <button  type="submit" class="btn btn-danger" value="delete">Delete</button></a>
                        </form>
                    </div>
                    <div class="col-sm-6">
                        <a href="/blogpost/create?id={{$post->id}}"><button  class="btn btn-primary">Edit</button></a>
                    </div>
                    </div>
                </div>
            </div>
        </div>

        <div style="margin:50px auto; width:50%">

            <h2 align="center">Latest Post</h2>
            @forelse($latests as $latest)
                <div class="post-container">
                <div class="post" style="padding:20px 35px;">
                <h3 class="post-title"><a href="/blogpost/{{$latest->id}}?{{$latest->title}}">{{$latest->title}}</a></h3>
                <div class="post-content">
                    <p>{{$latest->intro}}</p>
                </div>
                <div class="post-author">
                    <img src="{{$latest->user->getFileLink('photo')}}" alt="user profile pic">
                    <span>{{$latest->user->fullname}}</span>
                </div>
                </div>
                </div>

            @empty
                <div class="post-container">
                    <div class="post" style="text-align: center;">
                    Nothing here yet
                    </div>
                </div>
            @endforelse


        </div>

        @endsection

    If you go to `localhost/BlogPost/{post_id}` or just click on any post from the index page, you should see an output similar to the following:

    <img src="../images/demo_application_images/blog-output-3.png" />

1. For deleting a post, you need to send the delete request to the controller to execute the `destroy()` method, and your post will be deleted.

    For example, you can use the below code snippet to delete the post.

        <form method="Post" action="/blogpost/{{$post->id}}" >
        @csrf
        <input name="_method" type="hidden" value="DELETE">
        <button  type="submit" class="btn btn-danger" value="delete">Delete</button></a>
        </form>

    You need to pass the post ID in the URL- `/blogpost/{{$post->id}}` and include `" "` in the form.







