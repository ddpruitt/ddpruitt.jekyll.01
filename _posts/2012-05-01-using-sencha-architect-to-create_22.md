---
date: '2012-05-22T05:54:00.001-07:00'
description: ''
published: true
slug: 2012-05-using-sencha-architect-to-create_22
tags:
- ExtJS
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Using Sencha Architect to Create Grafted Tree
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2012/05/using-sencha-architect-to-create_22.html)*.

Clint Harris posted <a href="http://www.clintharris.net/2011/how-to-use-extjs-4-treepanels-with-both-static-data-and-model-stores/" title="How To Use ExtJS 4 TreePanels with Both Static Data and Model Stores">How To Use ExtJS 4 TreePanels with Both Static Data and Model Stores</a>.  He has a great explanation of how to "graft" branches onto an ExtJS TreeView.  In his example he is creating an Admin tree form that gives him access to Settings and Users.<br />
<br />
I recreated his project using <a href="http://www.sencha.com/products/architect/" target="_blank" title="Sencha Architect 2">Sencha Architect 2</a>.<br />
<br />
The trickiest part was getting the tree to load the data correctly.  I used the <strong>onLaunch</strong> function of the controller to get access to the TreeStores in order to call the userStore.setRootNode() and then to append the userStore to the settingsTreeStore.  <br />
<br />
Notice how I am using <strong>this.getUserTreeStoreStore()</strong> and <strong>this.getSettingTreeStoreStore()</strong>.  Yes, I had to use "StoreStore" because I named my stores UserTreeStore and SettingTreeStore, then the Controller tacks on the second "Store" when it creates the get function.<br />
<br />
<pre class="brush:javascript" name="code">
Ext.define('GraftedTreeApp.controller.TreePanelController', {
 extend: 'Ext.app.Controller',

 models: ['UserModel'],
 stores: [
 'SettingTreeStore',
 'UserTreeStore'
 ],

 onLaunch: function() {
  var userStore = this.getUserTreeStoreStore();
  userStore.setRootNode({
   text: 'Users',
   leaf: false,
   expanded: false
 });

  // Graft our userTreeStore into the settingsTreeStore. Note that the call
  // to .expand() is what triggers the userTreeStore to load its data.
  var settingsTreeStore = this.getSettingTreeStoreStore();
  settingsTreeStore.getRootNode().appendChild(userStore.getRootNode()).expand();
 }

});

</pre>

<br />
<br />
Pretty much everything else was setting properties in the Sencha Architect UI.  The project files are <a href="https://dl.dropboxusercontent.com/u/480457/techshorts/2012/05/graftedTree.zip">here</a>.<br />
<br />
<strong>NOTE:</strong> There is a known bug in this solution, when you collapse and expand the User node it loads more User data, after which the User node cannot be collapsed.