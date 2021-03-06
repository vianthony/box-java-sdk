Metadata Templates
==================

Metadata that belongs to a file is grouped by templates. Templates allow the metadata service to provide a multitude of services, such as pre-defining sets of key:value pairs or schema enforcement on specific fields. 

* [Create Metadata Template](#create-metadata-template)
* [Update Metadata Template](#update-metadata-template)
* [Get Metadata Template](#get-metadata-template)
* [Get Enterprise Metadata Templates](#get-enterprise-metadata-templates)
* [Delete Metadata Template](#delete-metadata-template)

Create Metadata Template
------------------------
The [`createMetadataTemplate(BoxAPIConnection, String, String, String, Boolean, List<Field>)`][create-metadata-template] method will create a metadata template schema.

You can create custom metadata fields that will be associated with the metadata template.

```java
MetadataTemplate.Field metadataField = new MetadataTemplate.Field();
metadataField.setType("string");
metadataField.setKey("text");
metadataField.setDisplayName("Text");

List<MetadataTemplate.Field> fields = new ArrayList<MetadataTemplate.Field>();
fields.add(metadataField);

MetadataTemplate template = MetadataTemplate.createMetadataTemplate(api, "enterprise", "CustomField", "Custom Field", false, fields);

final JsonObject jsonObject = new JsonObject();
jsonObject.add("text", "This is a test text");

Metadata metadata = new Metadata(jsonObject);
boxFile.createMetadata("CustomField", metadata);
```

[create-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#createMetadataTemplate(com.box.sdk.BoxAPIConnection,%20java.lang.String,%20java.lang.String,%20java.lang.Boolean,%20java.lang.List)

Update Metadata Template
------------------------

To update an existing metadata template, call the
[`updateMetadataTemplate(BoxAPIConnection api, String scope, String template, List<FieldOperation> fieldOperations)`][update-metadata-template]
method with the scope and key of the template, and the list of field operations to perform:

```java
List<MetadataTemplate.FieldOperation> updates = new ArrayList<MetadataTemplate.FieldOperation>();

String addCategoryFieldJSON = "{\"op\":\"addField\","\"data\":{"
    + "\"displayName\":\"Category\",\"key\":\"category\",\"hidden\":false,\"type\":\"string\"}}";
updates.add(new MetadataTemplate.FieldOperation(addCategoryFieldJSON));

String changeTemplateNameJSON = "{\"op\":\"editTemplate\",\"data\":{"
    + "\"displayName\":\"My Metadata\"}}";
updates.add(new MetadataTemplate.FieldOperation(changeTemplateNameJSON));

MetadataTemplate.updateMetadataTemplate(api, "enterprise", "myData", updates);
```

[update-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#updateMetadataTemplate-com.box.sdk.BoxAPIConnection-java.lang.String-java.lang.String-java.util.List-

Get Metadata Template
---------------------

The [`getMetadataTemplate(BoxAPIConnection)`][get-metadata-template-1] method will return information about default metadata schema.
Also [`getMetadataTemplate(BoxAPIConnection, String)`][get-metadata-template-2] and [`getMetadataTemplate(BoxAPIConnection, String, String, String...)`][get-metadata-template-3] can be used to set metadata template name, metadata scope and fields to retrieve.

```java
MetadataTemplate template = MetadataTemplate.getMetadataTemplate(api, "templateName");
```

[get-metadata-template-1]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(com.box.sdk.BoxAPIConnection)
[get-metadata-template-2]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(com.box.sdk.BoxAPIConnection,%20java.lang.String)
[get-metadata-template-3]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(com.box.sdk.BoxAPIConnection,%20java.lang.String,%20java.lang.String,%20java.lang.String...)


Get Enterprise Metadata Templates
---------------------------------

Calling the static [`getEnterpriseMetadataTemplates(BoxAPIConnection, String...)`][get-enterprise-metadata-1] will
return an iterable that will page through all metadata templates within a user's enterprise.
Also [`getEnterpriseMetadataTemplates(String, BoxAPIConnection, String...)`][get-enterprise-metadata-2] and [`getEnterpriseMetadataTemplates(String, int, BoxAPIConnection, String...)`][get-enterprise-metadata-3] can be used to set metadata scope, limit of items per single response.

```java
Iterable<MetadataTemplate> templates = MetadataTemplate.getEnterpriseMetadataTemplates(BoxAPIConnection api);
for (MetadataTemplate templateInfo : templates) {
    // Do something with the metadata template.
}
```

[get-enterprise-metadata-1]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(com.box.sdk.BoxAPIConnection,%20java.lang.String...)
[get-enterprise-metadata-2]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(java.lang.String,%20com.box.sdk.BoxAPIConnection,%20java.lang.String...)
[get-enterprise-metadata-3]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(java.lang.String,%20int,%20com.box.sdk.BoxAPIConnection,%20java.lang.String...)

Delete a Metadata Template
--------------------------

The ['deleteMetadataTemplate(BoxAPIConnection, String scope, String template)'][delete-metadata-template] method will remove a metadata template schema
from an enterprise.

```java
MetadataTemplate.deleteMetadataTemplate(api, "enterprise", "templateName");
```

[delete-metadata-template]: http://opensource.box.com/box-java-sdk/javadoc/com/box/sdk/MetadataTemplate.html#getEnterpriseMetadataTemplates(com.box.sdk.BoxAPIConnection,%20java.lang.String,$20java.lang.String)