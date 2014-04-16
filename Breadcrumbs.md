## Breadcrumbs

Want to display something useful in the breadcrumb of your
module on the front-office of the site? It's specified
in your templates and uses the `{capture}` feature of
Smarty:

```
    {capture name=path}
        {l s='Test'}
    {/capture}
```

This will create a breadcrumb with one unclickable link. If
you want the link to be clickable, surround the `{l}` with
an anchor tag:

```
    {capture name=path}
    <a href="#123">
        {l s='Test'}
    </a>
    {/capture}
```

If you want more than one item in the breadcrumb you have
to roll some of your own HTML:

```
    {capture name=path}
    	<a href="#root">
    		{l s='Root'}
    	</a>
    	
    	<span class="navigation_page">
    		{l s='Current Page'}
    	</span>
    {/capture}
```

I've seen a lot of modules that seem to use `$navigationPipe` which can
be modified from the PHP code of a module instead of in each template, so
you'll see code that does this:

```
    {capture name=path}
    	<a href="#root">
    		{l s='Root'}
    	</a>
    	
	<span class="navigation-pipe">
		{$navigationPipe}
	</span>
    	
    	<span class="navigation_page">
    		{l s='Current Page'}
    	</span>
    {/capture}
```

