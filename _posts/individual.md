# N@TM Reflection - A comprehensive analysis 🌍

- What went well

- What could be improved upon

- Common feedback

- Plans for CPT

- Other values gained by other teams

## What went well 🗼

At N@TM, all of the procedures went smoothly as planned. All of the features that we had planned for were working and a lot of people came by to check out our website. Some good techniques we had employed was a really cool homepage with aesthetics such as an RGB outline which people could spot from faraway. This attracted a lot of people to check out our project.

The like button was a huge hit among participants and so was the post hierarchy. It becaem a sort of post it board for the entire Night at the Museum. Our use of the other features such as the delete and the edit features also brung many to awe as there were questions about our backend which we proudly answered with our vast collection of knowledge.

As a team I think we did fine and indivudally I think I contriubted a lot to explaining to people how they backend works.

```
🔴🟡🟢                                            features.txt
______________________________________________________________________________________________________________________
1️⃣ Login Page                                    
2️⃣ Post feature                                  
3️⃣ Like feature                                  
4️⃣ Sign up feature                               
5️⃣ Delete feature                                
```

```py
import json, jwt
from flask import Blueprint, request, jsonify, current_app, Response
from flask_restful import Api, Resource # used for REST API building
from datetime import datetime
from auth_middleware import token_required

from model.users import User

user_api = Blueprint('user_api', __name__,
                   url_prefix='/api/users')


# API docs https://flask-restful.readthedocs.io/en/latest/api.html
api = Api(user_api)

class UserAPI:        
    class _CRUD(Resource):  # User API operation for Create, Read.  THe Update, Delete methods need to be implemeented
        @token_required
        def post(self, current_user): # Create method
            ''' Read data for json body '''
            body = request.get_json()
            
            ''' Avoid garbage in, error checking '''
            # validate name
            name = body.get('name')
            if name is None or len(name) < 2:
                return {'message': f'Name is missing, or is less than 2 characters'}, 400
            # validate uid
            uid = body.get('uid')
            if uid is None or len(uid) < 2:
                return {'message': f'User ID is missing, or is less than 2 characters'}, 400
            # look for password and dob
            password = body.get('password')
            dob = body.get('dob')
            ''' #1: Key code block, setup USER OBJECT '''
            uo = User(name=name, 
                      uid=uid)
            
            ''' Additional garbage error checking '''
            # set password if provided
            if password is not None:
                uo.set_password(password)
            # convert to date type
            if dob is not None:
                try:
                    uo.dob = datetime.strptime(dob, '%Y-%m-%d').date()
                except:
                    return {'message': f'Date of birth format error {dob}, must be mm-dd-yyyy'}, 400
            
            ''' #2: Key Code block to add user to database '''
            # create user in database
            user = uo.create()
            # success returns json of user
            if user:
                return jsonify(user.read())
            # failure returns error
            return {'message': f'Processed {name}, either a format error or User ID {uid} is duplicate'}, 400
        @token_required
        def get(self, current_user): # Read Method
            users = User.query.all()    # read/extract all users from database
            json_ready = [user.read() for user in users]  # prepare output in json
            return jsonify(json_ready)  # jsonify creates Flask response object, more specific to APIs than json.dumps

        
        def put(self, user_id):
            '''Update a user'''
            user = User.query.get(user_id)
            if not user:
                return {'message': 'User not found'}, 404
            body = request.get_json()
            user.name = body.get('name', user.name)
            user.uid = body.get('uid', user.uid)
            db.session.commit()
            return user.read(), 200

        def delete(self, user_id):
            '''Delete a user'''
            user = User.query.get(user_id)
            if not user:
                return {'message': 'User not found'}, 404
            db.session.delete(user)
            db.session.commit()
            return {'message': 'User deleted'}, 200
    
    class _Security(Resource):
        def post(self):
            try:
                body = request.get_json()
                if not body:
                    return {
                        "message": "Please provide user details",
                        "data": None,
                        "error": "Bad request"
                    }, 400
                ''' Get Data '''
                uid = body.get('uid')
                if uid is None:
                    return {'message': f'User ID is missing'}, 400
                password = body.get('password')
                
                ''' Find user '''
                user = User.query.filter_by(_uid=uid).first()
                if user is None or not user.is_password(password):
                    return {'message': f"Invalid user id or password"}, 400
                if user:
                    try:
                        token_payload = {
                            "_uid": user._uid,
                            "role": user.role 
                        }
                        token = jwt.encode(
                            token_payload,
                            current_app.config["SECRET_KEY"],
                            algorithm="HS256"
                        )
                        resp = Response("Authentication for %s successful" % (user._uid))
                        resp.set_cookie("jwt", token,
                                max_age=3600,
                                secure=True,
                                httponly=True,
                                path='/',
                                samesite='None'  # This is the key part for cross-site requests

                                # domain="frontend.com"
                                )
                        return resp
                    except Exception as e:
                        return {
                            "error": "Something went wrong",
                            "message": str(e)
                        }, 500
                return {
                    "message": "Error fetching auth token!",
                    "data": None,
                    "error": "Unauthorized"
                }, 404
            except Exception as e:
                return {
                        "message": "Something went wrong!",
                        "error": str(e),
                        "data": None
                }, 500
    class Login(Resource):
        def post(self):
            data = request.get_json()

            uid = data.get('uid')
            password = data.get('password')

            if not uid or not password:
                response = {'message': 'Invalid creds'}
                return make_response(jsonify(response), 401)

            user = User.query.filter_by(_uid=uid).first()

            if user and user.is_password(password):
         
                response = {
                    'message': 'Logged in successfully',
                    'user': {
                        'name': user.name,  
                        'id': user.id
                    }
                }
                return make_response(jsonify(response), 200)

            response = {'message': 'Invalid id or pass'}
            return make_response(jsonify(response), 401)
    class _Create(Resource):
        def post(self):
            body = request.get_json()
            # Fetch data from the form
            name = body.get('name')
            uid = body.get('uid')
            password = body.get('password')
            role = body.get('role')
            if uid is not None:
                new_user = User(name=name, uid=uid, password=password, role=role)
            user = new_user.create()
            if user:
                return user.read()
            return {'message': f'Processed {name}, either a format error or User ID {uid} is duplicate'}, 400
    class _Delete(Resource):
        def post(self): # Delete Method
            body = request.get_json()
            uid = body.get('uid')
            password = body.get('password')
            user = User.query.filter_by(_uid=uid).first()
            if user is None or not user.is_password(password):
                return {'message': f'User {uid} not found'}, 404
            json = user.read()
            if user:
                try:
                    user.delete() 
                except Exception as e:
                    return {
                        "error": "Something went wrong!",
                        "message": str(e)
                    }, 500
            # 204 is the status code for delete with no json response
            return f"Deleted user: {json}", 204 # use 200 to test with Postman
            
    # building RESTapi endpoint
    api.add_resource(_CRUD, '/')
    api.add_resource(_Security, '/authenticate')
    api.add_resource(Login, '/login')
    api.add_resource(_Create, '/create')
    api.add_resource(_Delete, '/delete')
```


## What we could have improved on

For the purpose of CPT, our project needed a more direct purpose. The purpose was the main issue we had going into the project. We found out that we needed an actual purpose to fulfill and instead of looking at that we started to focus way more on fucntionality. This was good as it helped us move forward for our night at the museum endeavors, but for actual CPT it might be more helpful to actually have a goal in mind. I think some edits which might need to be made to make this an actual good CPT project is a target audience. Maybe the corporate world or just plain consumers. The consumer must be in mind in order to find a goal or purpose.

## Common feedback

Here are some common feedback I got about the project as I conversed with those who attended the event:

- Maybe try adding a Direct Message option

- Try adding a way to post images and videos

- Try adding an embed system

- Make replies more visible

- Try adding threads to make replying more streamlined

- Maybe add buitlin features the user could use for more interaction like built-in survey mode

## Plans for CPT

There are two plans I have for CPT. Plan 1 is to build off on this current CPT project and add all of the features I am thinking of. On top of that, the feedback features could also be added. Although the drawback of this is that part of whther I really want to present a web design project to College Board like everyone or not?

If the entire Del Norte is submitting a server wit flask backend as a part of CPT, I need to make something which deviates me form others. Something which can get me a 5. So I can do this by these 3 ideas:


### 1. Extend Bluejay CPT 🐦🐧

Possible Features:

- Image upload

- DMs

- Video upload

- Refined purpose

### 2. Extending Orion RSH (my personal project form trimester 1) and adding some more features ✈️🌍

Possible Features:

- PAM support

- More configurations

- More support for plugins (will naturally help with security granting possible use for corporate benefit)

- Taylor per rubric

### Plan for CollegeBoard MCQ 📃

- Research more on my own away from web development related subjects

- Refine my coding skills in terms of knowledge

### Orion RSH plan 🚀

- Implement PAM support

- Try to maybe use skills from web development to create a distinct UI

- Make better configurations and parsing

### My CPT contributions

For my team, I deployed our backend, I made the MessageAPI feature, and the Like feature. I also did more things, but htese were my key commits. OVerall, I feel like I have acted as a satisfactory Backend operator.

My contributions are documented in the video above.