The first parameter defines a prefix from which all assets contained in this collection may be fetched.

The second parameter defines the compression used for the assets, as presented within the [Content-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Encoding) header. Acceptable value could be `gzip` or `br`. Note that [BuiltinAssets] does not compress the assets for you: this parameter is merely used for you to advertise wihch compression you may already have applied on the assets that this collection will be filled with.

The second parameter may also be left empty, meaning the assets within this collection have not been compressed.
