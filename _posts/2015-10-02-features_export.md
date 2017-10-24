---
title: "Errors on features export"
layout: single
category:
date: 2015-10-02 10:13:42 BST
published: true
tags:
- drupal
---

Had a strange error being reported when exporting features from a Drupal 7 instance, in that the resultant tar file was not extracting using any of the usual tools, such as tar etc.

```bash
$ file features_export-7.x-1.0-alpha1.tar
features_export-7.x-1.0-alpha1.tar: data
```

File magic showed that the file was wrong, but looking at the file itself looked correct at first glance, and a look around on Drupal.org returned [this](https://www.drupal.org/node/522794) old thread which lead me to

```bash
$ head features_export-7.x-1.0-alpha1.tar

features_export/features_export.features.conditional_fields.inc^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@100644 ^@   765 ^@   765 ^@     557662 12603173414^@021333^@ ^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@ustar  ^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@^@<?php
```

The key being the blank first line in the above file, eventually tracked the following to the following in ```settings.php```:

```php
$ head settings.php

<?php
$databases = array (
  'default' =>
  array (
```

Remove the blank line before the opening php tag and tar file successfully generates and can be extracted:

```bash
$ file features_export-7.x-1.0-alpha1.tar
features_export-7.x-1.0-alpha1.tar: POSIX tar archive (GNU)
```
