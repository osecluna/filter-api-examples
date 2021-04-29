# filter-api-examples

## Installing the content types and schemas on your hub
```
npm install -g @amplience/dc-cli

dc-cli configure --clientId <YOUR_CLIENT_ID> --clientSecret <YOUR_CLIENT_SECRET> --hubId <YOUR_HUB_ID>

dc-cli content-type-schema import content-type-schemas

dc-cli content-type import content-types

```

### Example filter API requests

All the below examples use the content delivery 2 endpoint ```/content/filter ```

#### List by schemaId: List blog posts

```
{
		"filterBy": [{
			"path": "/_meta/schema",
			"value": "https://schema-examples.com/blogpost-filter-and-sort"
		}]
}
```

#### Sorting: List blog posts, sorted by date

```
{
		"filterBy": [{
			"path": "/_meta/schema",
			"value": "https://schema-examples.com/blogpost-filter-and-sort"
		}],
		"sortBy": {"key": "default", "order": "DESC"}
}
```

#### Multiple filters: List blog posts, filtered by category

Multiple filters will always be AND logic

```
{
	"filterBy": [{
		"path": "/_meta/schema",
		"value": "https://schema-examples.com/blogpost-filter-and-sort"
	},
	{
		"path": "/category",
		"value": "Women"
	}]
}
```

#### List by parentId: List hierarchy child nodes, sorted by title

Substitute value with the contentItemId of the parent hierarchy node

Sort key 'title' is defined in the schema blog-hierarchy.json

```
{
	"filterBy": [{
		"path": "/_meta/hierarchy/parentId",
		"value": "3bf04259-84d3-44a2-9c80-ce1b07085f59"
	}],
	"sortBy": {"key": "default", "order": "DESC"}
}
```

#### Paging - custom size: List hierarchy child nodes, page size of 4

```
{
	"filterBy": [{
			"path": "/_meta/hierarchy/parentId",
		  "value": "3bf04259-84d3-44a2-9c80-ce1b07085f59"
	}],
  	"page": {
    		"size": 4
  	}
}
```

#### Paging - next page: List hierarchy child nodes, request next page

Substitute cursor value with nextCursor value returned in previous response

```
{
	"filterBy": [{
			"path": "/_meta/hierarchy/parentId",
		  	"value": "3bf04259-84d3-44a2-9c80-ce1b07085f59"
	}],
  	"page": {
    		"size": 4,
		"cursor": "eyJzb3J0S2V5IjoiXCIgNCIsIml0ZW1JZCI6ImJsb2Jsb2ctaHViLTAxOjQwMTAxNzdjLTFhZmMtNGM4ZC1iMTU5LWZlOGE4NWIyZjcwNyJ9"
  	}
}
```

#### Boolean value: List PDP content blocks where hidden is false and categoryId is mens-clothing-suits, sorted by priority, page size of 3

```
{
	"filterBy": [
		{
			"path": "/_meta/schema",
			"value": "https://schema-examples.com/pdp-content-block"
		},
		{
			"path": "/hidden",
			"value": false
		},
		{
			"path": "/categoryId",
			"value": "mens-clothing-suits"
		}],
	"sortBy": {"key": "default", "order": "DESC"},
	"page": {
    		"size": 3
  	}
}
```
