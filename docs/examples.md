
Example cases for the API.

*Descriptors generation:*

* taking the descriptors from any image provided, the image is specified via URL.

GENERATE or POST to:
/descriptors/
```json
{
"image_url": "/local/path/to/image.jpg",
"extraction_type": "general_image"
}
```
Can you deal with remote URLs, like "http://example.net/path/to/image.png"? Not necessary.
What image types can you handle? We can convert e.g. to JPEG, but we shall know it.
What is the exact of the descriptors we get? Is it e.g. array of flow-point numbers from [0,1] interval?

*Regular indexes:*

* Here we need to put image descriptor-hashes into the m-index, and do the common (check, delete, search) stuff along with it.
Notice that we have the _provider_ property in. It is used for (kind of dynamic) segmenting of the index.
Several customers of ours would share a single index instance.

PUT to:
/index/{index_id}/image/{image_id}
```json
{
"provider": "customer_abcd",
"mage_hash": [0.1, 0.9, 0.8, 0.2, ..., 0.7]
}
```

SEARCH or POST to:
/index/{index_id}/image/
{
"method": "even_weights_for_structures_and_colors",
"count": 20,
"providers": ["provider_abcd", "provider_efgh", ..., "provider_rstu"],
"image_hashes": [[0.1, ..., 0.7], [0.6, ..., 0.2], ..., [0.4, ..., 0.5]]
}

We need to specify which providers are amenable for the search, as several providers (i.e. customers of ours)
shall share the same index instance.
If it would be possible to specify several (i.e. more than one) images for the serch, would be nice, but probably
not necessary in the first iteration.
Probably not possible to specify an offset, as for pagination, in a way that it would be efficient.
Could we have an estimation for a minimal count of images in an index when it provides satisfiable results, i.e. reasonably similar images?

*Tags index:*

* This index would be precriated and only used for tag-suggesting.

SUGGEST or POST to:
/index/{index_id}/tags/
{
"image_hashes": [[0.1, ..., 0.7], [0.6, ..., 0.2], ..., [0.4, ..., 0.5]]
}

If it would be possible to specify several (i.e. more than one) images for the suggestion, would be nice, but probably
not necessary in the first iteration.

