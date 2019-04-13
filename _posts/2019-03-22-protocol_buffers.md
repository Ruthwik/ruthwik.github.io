---
layout: post
title: Protocol Buffers 101
subtitle: Under Contruction.
published: true
categories: other```
```
tags: [protobuff, gRPC]

bigimg:
  - /img/protobuf/homepage.jpg

---


<p>
<code>Serialization</code> is the process of converting an object into a stream of bytes to store the object or tranfer over a network. Its main purpose is to save the state of an object in order to be able to recreate it when needed. The reverse process is called deserialization. There are various ways to achieve serialization/deserialization like JSON, XML, Avro or in Java using Serializable interface. This post is about Protocol Buffers which started gaining popularity in the recent years for its efficient serialization and deserialization.
</p>
<img src="/img/protobuf/docker_core.jpg" alt="serialization" height="50%" width="50%">
<p>

<h3>Protocol Buffers</h3>
Protocol Buffers are developed by Google. It is an extensible serialization technique for the structured data. Once the structured data is defined, then source code can be generated to easily read and write the data using variety of languages. The main adavantage of using protobuf is backaward and forward compatibility.

<img src="/img/protobuf/docker_core.jpg" alt="proto" height="50%" width="50%">

Specify the structured data that you want to serialize by defining protocol buffer message types in .proto specification file. Each protocol buffer message is a small logical record of information.
From the proto file, the protocol buffer compiler will generate a class that can be used in an application to serialize and deserialize.


</p>


<h3>Basics</h3>
<h4>Defining the first message</h4>
<h4>Types</h4>
<p>A message field can have one of the following types – Can see the complete list here
https://developers.google.com/protocol-buffers/docs/proto#scalar
<ul>
	<li> <strong><em>Number :</em></strong> double,float, int32 ,int64, unit32 ..... are used as field type</li>
	<li> <strong><em>Boolean :</em></strong> 'bool' is used in the field type when you want a field with boolean type</li>
	<li> <strong><em>String :</em></strong> 'string' is used for string tyoe. A string must always contain UTF-8 encoded or 7 bit ASCII text</li>
  <li> <strong><em>Bytes :</em></strong> 'bytes' is used for any sequence of byte array.</li>
</ul></p>
<p><strong><em>Importing types</em></strong>
Types can be imported defined in a different .proto files or when you want to use re-use code and import other .proto files created by people
</p>

```Java
import "date.proto";
```

<h4>Tag</h4>
<p>Tag is the most important element. The smallest being 1 and largest being 2<sup>19</sup> - 1 .
We cannot use the numbers from 19000 to 19999 since they are reserved. Tags numbered from 1 to 15 use 1 byte in space and from 16 to 2047 use 2 bytes.</p>

```
 string first_name = 1;
 string last_name = 2;
```
<h4>Repeated fields</h4>
<p>The repeated fields are used to  make a 'list' or an 'array'. The list can take any number (o or more) of elements.The opposite of repeated is singular.</p>

```
repeated string numbers;
```
<h4>Default values</h4>
<p>All fields will take a default value when not specified.
<ul>
	<li>bool: false</li>
	<li>number (int32): 0</li>
  <li>string: empty string</li>
  <li>bytes: empty bytes</li>
  <li>enum: first value</li>
  <li>repeated: empty list</li>
</ul>
</p>

</p>
<h4>Enum</h4>
<p>You can use enum when you know all the values a field can take in advance. The first value of enum is the default value. It must start by the tag 0.
</p>

```
enum Eyecolor {
  UNKNOWN_EYE_COLOR = 0;
  EYE_GREEN = 1;
  EYE_BROWN = 2;
};
```

<h4>Package</h4>
<p>The protobuf compiler places the code at the package indicated. It prevents name conflicts between the messages.
</p>

```
package date;
```


<h3>Rules for Updating Protocol Buffers</h3>
<ul>
	<li>The numeric tags should not be changes for any existing fields</li>
	<li>New fields can be added and the old code will just ignore them.</li>
  <li>Likewise, if the old/new code reads unknown data, the default will take place.</li>
  <li>Fields can be removed as long as the tag number is not used again in the
  updated message typeYou may want to rename the field instead,
  perhaps adding the prefix "OBSOLETE_" or make the tag reserved, so that
  future users of the proto can't accidentally resuse the numner</li>
  <li>Default values should be used with car. </li>
</ul>

> Defaults are tricky to deal with. They allow protobuf to easily evolve without breaking any existing or new codes. They also ensure the a field will always have a non null values.  They are dangerous too because you cannot differentiate from a missing field or if a value equal to the default was set. The most important note is
the default value shouldn't have any meaning in the business.

<h4>Adding Fields</h4>
<p>The tag number ensures the forward and the backward compatibility. After adding a new field,
if it is sent to old, the old code will not know what the tag numbers corresponds to and the field will be ignored or dropped. This ensures backward compatibility. Oppositely, if we read the old data with the new code, the new field will not be found and the default value will be assumed (empty string, empty list etc...).
</p>
<img src="/img/protobuf/docker_core.jpg" alt="add_fields" height="50%" width="50%">

<h4>Renaming Fields</h4>
<p>The field names can be changed freely. The tag number is the most important in protobuf.
</p>

<img src="/img/protobuf/docker_core.jpg" alt="rename_field" height="50%" width="50%">

<h4>Removing Fields</h4>
<p>A field can be removed when it is not required anymore. If the old code doesn't find the field anymore, the default will be used. Oppositely, if we read the old data with the new code, the deleted dield will be just be dropped.
</p>
<strong><em>Removing Fields: Reserved Tags</em></strong>
<p>When removing a field, you should always reserve the tag and the name. This prevents the tag to be
re-used. This is necessary to prevent conflcits in the codebase</p>

<p>The alternatives is that insteas of removing a field it can be renamed to OBSOLETE_field_name. The downsode is that you may have to populate that field while your client gets upgraded to use the newer field that replaces it (which has a new tag).
</p>
<h4>Reserved Keywords</h4>
<p>Tags and field names are reserved to prevent new fields from re using the tags. Tags and field names
can't be mixed in the same reserved statment.</p>


```
message Student{
  reserved 2, 5 , 10 to 12;
  reserved "name" , "mail";
}
```
> Do not remove any reserved tags ever.

<h3>Advanced Types</h3>
<p>
</p>
<h4>Oneof</h4>
<p>
</p>
<h4>Maps</h4>
<p>
</p>
<h4>Timestamp</h4>
<p>
</p>
<h4>Duration</h4>
<p>
</p>
<h3>Example</h3>
<p>
</p>
<h4>Defining the Protocol Buffers</h4>
<p>
</p>
<h4>Compiling the Protocol Buffers</h4>
<p>
</p>

<p>
I have used the following references and sometimes used the same explanation. Do check the following resources for more understanding.

	<ul>
      <li><a href="https://developers.google.com/protocol-buffers/docs/overview">Offical Google's Protocol Buffer documentation</a></li>
      <li><a href="https://github.com/lazarofl/protocvsjsoncomparison"> Proto vs JSON comparison</a></li>
  </ul>
</p>

<p>If you have any question or feedback, please do reach out to me by commenting below.</p>
