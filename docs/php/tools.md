---
layout: post
title:  tools
date:   2022-06-24 20:31:00 +0800
categories: php doc
parent: PHP
nav_order: 2
---


# PHP 常用方法

1. 递归父子树
	
	```php
	function buildTree($elements = [], $parentId = 0) {
	    $branch = [];

	    foreach ($elements as $item) {
	        if ($item['parent_id'] == $parentId) {
	            $children = buildTree($elements, $item['id']);
	            if ($children) {
	                $item['children'] = $children;
	            }
	            $branch[] = $item;
	        }
	    }

	    return $branch;
	}
	```

2. 递归数加节点
	```php
	function loopTree(&$elements = [], $level = 0)
    {
        $level++;
        foreach ($elements as &$item) {
            $item['level'] = $level;
            if (!empty($item['children'])) {
                loop_tree($item['children'], $level);
            }
        }

        return $elements;
    }
	```