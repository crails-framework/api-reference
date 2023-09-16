Adds a recipient to the mail.

You must specify an address for the recipient, and you may also optionally specify a name which will help identify the owner of the address.

The `flags` parameter can be use to determine the type of the recipient, using the [Mail::RecipientType] enum.

Using `Mail::CarbonCopy` as a flag, the aforementionned recipient will receive the mail as a copy, rather than as the main recipient.

Using `Mail::CarbonCopy | Mail::Blind` as a flag will result in a similar effect, though the recipient will be hidden from all other recipients, which is good practice when sending the same mail to multiple users.

_N.B.: a Mail must have at least one recipient that's neither a Carbon Copy or a Blind Carbon Copy recipient. A common trick to work around this issue is to use the sender's email as a normal recipient, and then specifying all our other recipients as Blind Carbon Copy recipients._
