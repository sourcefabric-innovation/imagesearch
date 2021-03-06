Example cases for the API
-------------------------

**Descriptors generation:**


Taking the descriptors from any image provided, the image is specified via URL.

GENERATE or GET to:
/descriptors/
```json
{
"image_url": "/local/path/to/image.jpg",
"extraction_type": "general_image"
}
```

* Can it deal with remote URLs, like "http://example.net/path/to/image.png"? Though it is not necessary.
* What image types can it handle? We can convert e.g. to JPEG, but we shall know it.
* What is the exact of the descriptors we get? Is it e.g. array of flow-point numbers from [0,1] interval?

**Regular indexes:**

Here we need to put image descriptor-hashes into the m-index, and do the common (check, delete, search) stuff along with it.
Notice that we have the *provider* property in (it is used instead of regular tags). It is used for (kind of dynamic) segmenting of the index.
Several customers of ours would share a single index instance, and they can make various agreements on image sharing.

PUT to:
/index/{index_id}/image/{image_id}
```json
{
"provider": "customer_abcd",
"mage_hash": [0.1, 0.9, 0.8, 0.2, ..., 0.7]
}
```

SEARCH or GET to:
/index/{index_id}/image/
```json
{
"method": "even_weights_for_structures_and_colors",
"count": 20,
"providers": ["provider_abcd", "provider_efgh", ..., "provider_rstu"],
"image_hashes": [[0.1, ..., 0.7], [0.6, ..., 0.2], ..., [0.4, ..., 0.5]]
}
```

* We need to specify which providers are amenable for the search, as several providers (i.e. customers of ours)
shall share the same index instance.
* If it would be possible to specify several (i.e. more than one) images for the search, it would be nice, but probably
not necessary in the first iteration.
* Probably not possible to specify an offset, as for pagination, in a way that it would be efficient.
* Could we have an estimation for a minimal count of images in an index when the system provides satisfiable results, i.e. reasonably visually similar images?

**Tags index:**

This (static) index would be precreated and only used for tag-suggesting.

SUGGEST or GET to:
/index/{index_id}/tags/
```json
{
"image_hashes": [[0.1, ..., 0.7], [0.6, ..., 0.2], ..., [0.4, ..., 0.5]]
}
```

* If it would be possible to specify several (i.e. more than one) images for the suggestion, would be nice, but probably
not necessary in the first iteration.

