# Summernote Plugin elFinder
Summernote Plugin for elFinder File Manager

## Installation
- Download plugin files. Extract it and copy into your summernote plugin directory.
- Include the summernote ext javascript file into your html page.
- Includes code for images and file links. Note that your copy of Summernote must 

    ```javascript
    <script src="path/to/plugin/summernote-ext-elfinder/summernote-ext-elfinder.js"></script>
    ```


- Initialize the plugin at your summernote initialization code.

    ```javascript
    <script type="text/javascript">
      $(function() {
        $('.summernote').summernote({
          height: 200,
          tabsize: 2,
          toolbar: [
              ['style', ['bold', 'italic', 'underline', 'clear']],
              ['insert', ['elfinder']]
            ]
        });
      });
      function elfinderDialog() {
      	var fm = $('<div/>').dialogelfinder({
      		url : 'https://path.to/your/connector.php', // change with the url of your connector
      		lang : 'en',
      		width : 840,
      		height: 450,
      		destroyOnClose : true,
      		 getFileCallback : function(file, fm) {
                console.log(file);
                var link_url = fm.convAbsUrl(file.url);
                // Use line below if you want a root relative url
                // Your summernote copy must contain the changes noted at the link below for root relative link to work.
                // https://github.com/summernote/summernote/pull/2971
                // var link_url = link_url.substring(link_url.indexOf('/', 8));
				if (file.mime.substring(0,6) == 'image/') {
	                context.summernote('editor.insertImage', link_url);
				} else {
					var linkInfo = {
						url:link_url,
						text:file.name,
						isNewWindow:false
					}
					context.summernote('editor.createLink', linkInfo);
				}
            }
      		commandsOptions : {
      			getfile : {
      			oncomplete : 'close',
      			folders : false
      			}
      		}
      	}).dialogelfinder('instance');
      }
    </script>
    ```

## Tested with
- Summernote : v0.8.10 for Bootstrap 4
- elFinder : 2.1.42
- Bootstrap : v4.1.3
- jQuery : v3.3.1
- jQuery-UI : v1.12.1

## NOTE :
Don't forget to include the jQuery and jQuery-UI. The latest elFinder not include jquery-ui file.
