---
layout: post
title: How to copy extra files when publish web application in Visual Studio
image: /img/blog/publish.jpg
tags: [visual studio, deployment]
---
<p>The robust deployment procedure should be using msbuild to build the project, however for a small website application, we can just edit the publish file to include the custom files that is not included in the project solution.</p>
<p>First, you need to update the publish profile file below the properties folder which is:</p>
<p><img style="width: 215px; height: 107px;" src="/img/blog/publish_vs.jpg?width=215px&amp;height=107px" alt="" rel="3974" /></p>
<p>Then open and edit as below:</p>
<pre class="prettyprint prettyprinted"><span class="tag"><br />&lt;Target </span><span class="atn">Name</span><span class="pun">=</span><span class="atv">"CustomCollectFiles"</span><span class="tag">&gt;<br /></span><span class="tag">   &lt;ItemGroup&gt;</span><span class="pln">
      &lt;_CustomFiles Include="..\ExtraFiles\**\*" /&gt;
      </span><span class="tag">&lt;FilesForPackagingFromProject </span><span class="atn">Include</span><span class="pun">=</span><span class="atv">"%(_CustomFiles.Identity)"</span><span class="tag">&gt;<br /></span><span class="tag">           &lt;DestinationRelativePath&gt;</span><span class="pln">%(RecursiveDir)%(Filename)%(Extension)</span><span class="tag">&lt;/DestinationRelativePath&gt;<br /></span><span class="tag">      &lt;/FilesForPackagingFromProject&gt;<br />   </span><span class="tag">&lt;/ItemGroup&gt;<br /></span><span class="tag">&lt;/Target&gt;<br />&lt;PropertyGroup&gt;<br />   &lt;CopyAllFilesToSingleFolderForPackageDependsOn&gt;<br />     CustomCollectFiles;<br />     $(CopyAllFilesToSingleFolderForPackageDependsOn);<br />   &lt;/CopyAllFilesToSingleFolderForPackageDependsOn&gt;<br />  &lt;CopyAllFilesToSingleFolderForMsdeployDependsOn&gt;<br />    CustomCollectFiles;<br />    $(CopyAllFilesToSingleFolderForPackageDependsOn);<br />  &lt;/CopyAllFilesToSingleFolderForMsdeployDependsOn&gt;<br /> &lt;/PropertyGroup&gt;<br /><br /></span></pre>
<p> </p>
<p>Reference:</p>
<p>http://www.asp.net/mvc/overview/deployment/visual-studio-web-deployment/deploying-extra-files</p>