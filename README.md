Yii2 Cropper
===========
Yii-Framework extension for uploading and cropping images.

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
composer require specialist/yii2-cropper "dev-master"
```

or add

```
"specialist/yii2-cropper": "dev-master"
```

to the require section of your `composer.json` file.

Usage
-----

Once the extension is installed, simply use it in your code by  :

```
use specialist\cropper\CropperWidget;
```


```
<?php $form = ActiveForm::begin(['id' => 'form-profile']); ?>
    <?php echo $form->field($model, 'photo')->widget(CropperWidget::className(), [
        'uploadUrl' => Url::toRoute('/controller-name/upload-photo'), // 'uploadUrl' => Url::toRoute('/category/upload-photo')
        'width' => 300,
        'height' => 300,
    ]) ?>
    <div class="form-group">
        <?php echo Html::submitButton('Save', ['class' => 'btn btn-primary']) ?>
    </div>
<?php ActiveForm::end(); ?>
```
Widget has following properties:

| Name     | Description    | Default |  Required   |
| --------|---------|-------|------|
| uploadParameter  | Upload parameter name | file    |No |
| width  | The final width of the image after cropping | 200    |No |
| height  | The final height of the image after cropping | 200    |No |
| label  | Hint in box for preview | It depends on application language. You can translate this message on your language and make pull-request.    |No |
| uploadUrl  | URL for uploading and cropping image |     |Yes |
| noPhotoImage  | The picture, which is used when a photo is not loaded. | You can see it on screenshots in this instructions   |No |
| maxSize  | The maximum file size (kb).  | 2097152    |No |
| cropAreaWidth  | Width box for preview | 300    |No |
| cropAreaHeight  | Height box for preview | 300    |No |
| aspectRatio | Fix aspect ratio of cropping area | null |No |
| extensions  | Allowed file extensions (string). | jpeg, jpg, png, gif    |No |


In UserController:

```
use specialist\cropper\actions\UploadAction;
```

```
public function actions()
{
    return [
        'upload-photo' => [
            'class' => UploadAction::className(),
            'url' => '../../uploads/',  //you must create 'uploads' directory in your root directory -> '../../uploads/categories/'
            'path' => '../../uploads/', //you must create 'uploads' directory in your root directory
        ]
    ];
}
```
Action has following parameters:

| Name     | Description    | Default |  Required   |
| --------|---------|-------|------|
| path  | Path for saving image after cripping |     |Yes |
| url  | URL to which the downloaded images will be available. |  |Yes |
| uploadParameter  | Upload parameter name. It must match the value of a similar parameter of the widget. | file    |No |
| maxSize  | The maximum file size (kb). It must match the value of a similar parameter of the widget. | 2097152    |No |
| extensions  | Allowed file extensions (string). It must match the value of a similar parameter of the widget. | jpeg, jpg, png, gif    |No |
| width  | The final width of the image after cropping. It must match the value of a similar parameter of the widget. | 200    |No |
| height  | The final height of the image after cropping. It must match the value of a similar parameter of the widget. | 200    |No |
| jpegQuality  | Quality of cropped image (JPG) | 100    |No |
| pngCompressionLevel  | Quality of cropped image (PNG) | 1    |No |
