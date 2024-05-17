<!--yml
category: 未分类
date: 2024-05-18 05:46:37
-->

# Protocol Buffer – Backward Compatibility | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/09/16/protocol-buffer-backward-compatibility/#0001-01-01](https://mdavey.wordpress.com/2014/09/16/protocol-buffer-backward-compatibility/#0001-01-01)

## Protocol Buffer – Backward Compatibility

Worth [remembering](https://developers.google.com/protocol-buffers/docs/javatutorial):

*   you must not change the tag numbers of any existing fields.
*   you must not add or delete any required fields.
*   you may delete optional or repeated fields.
*   you may add new optional or repeated fields but you must use fresh tag numbers (i.e. tag numbers that were never used in this protocol buffer, not even by deleted fields).

~ by mdavey on September 16, 2014.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)