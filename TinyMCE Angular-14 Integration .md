#     **TinyMCE Angular-14 Integration**

**Steps**

- Install the tinymce-angular package and save it to your package.json with --save.

    ``` 
          npm install --save @tinymce/tinymce-angular
    ```
- Using a text editor, open /path/to/tinymce-angular-demo/src/app/app.module.ts and
  
   ``` import { BrowserModule } from '@angular/platform-browser';
       import { NgModule } from '@angular/core';
       import { EditorModule } from '@tinymce/tinymce-angular';
       import { AppComponent } from './app.component';

       @NgModule({
         declarations: [
           AppComponent
         ],
         imports: [
           BrowserModule,
           EditorModule
         ],
         providers: [],
         bootstrap: [AppComponent]
       })
       export class AppModule { } 
   ```
 - Using a text editor, open /path/to/tinymce-angular-demo/src/app/app.component.html and replace the contents with
 
  ```
      <h1>TinyMCE 5 Angular Demo</h1>
      <editor
         apikey=”your api key”
         [init]="{
           height: 500,
           menubar: false,
           plugins: 'Lists advlist’,
           toolbar:
             'undo redo formatselect bold italic backcolor \
             alignleft aligncenter alignright alignjustify \
             bullist numlist outdent indent removeformat'
            }">
        </editor>
  ```
  
  This TinyMCE editor configuration should output the basic tinymce editor
  To render the content of the TinyMCE in the HTML we should use innerHTML binding like the following…
  
  Let us assume content is a variable that represents the content of TinyMCE         
 ```             
               <div [innerHTML]=”content”> </div>
 ```
 But at this time we may face a problem in seeing the effect of TinyMCE    styling effect this is due to the security issue of innerHTML tagging. 
 To slove this problem we need to apply the following steps
 
- Import this module in our html component
```
    import { DomSanitizer } from '@angular/platform-browser';
```
- In .ts file update the constructor using domsanitizer instance
```
     Constructor{public sanitizer: DomSanitizer}
```
- And then initialize our content in the constructor
```
     Content = sanitizer.byPassSecurityTrustHtml(content) 
```
 Now we can render the TinyMce content with all styling with no problem
 
