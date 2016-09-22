   function generateXml(outElement, srcElement) {
            removeChild(outElement);

            var ident = '15px', _id;
            var cName = 'leftmargin';

            var oElement = outElement || document.createDocumentFragment();

            generateTree(srcElement);

            function generateTree(srcElement) {
                srcElement = $(srcElement);
                if (srcElement.contents().length > 0) {
                    var temp = appendParent(oElement, $(srcElement).get(0));
                    oElement = temp || oElement;
                    srcElement.contents().each(function (i, e) {
                        generateTree(e);
                    });
                    oElement = findRoot(oElement.parentElement);
                }
                else {
                    var temp = appendChild(oElement, $(srcElement).get(0));
                    oElement = findRoot(temp);
                }
            }

            function findRoot(el) {
                var e = el;
                while (true) {
                    try {
                        var c = e.className;
                        if (c.indexOf('xmlChildren') >= 0) {
                            break;
                        }
                        else if (e.id === 'xmlTree') { return e; }
                        else if (e.id === 'section2') {return e.children[0];}
                    }
                    catch (e) { return e; }


                    e = e.parentElement;
                }
                return e;
            }
            function addSpanNode(parent, text, className) {
                var newNode = document.createElement('span');
                if (className) { newNode.className = className; }
                if (text) { newNode.appendChild(document.createTextNode(text)); }
                if (parent) { parent.appendChild(newNode); }
                return newNode;
            }
            function createTextNode(parent, text) {
                var txt = document.createTextNode(text);

                if (parent) parent.appendChild(txt);
                return txt;
            };


            function createNode(nodeName, className) {
                if (nodeName) {
                    var node = document.createElement(nodeName);
                    if (className)
                        node.className = className;
                    return node;
                }

                else
                    return null;
            }

            function appendChild(parent, nodeToInsert, isParent) {

                var parentDiv = createNode('div');
                var div = createNode('div', cName);
                div.id = _id;

                //start 
                if (nodeToInsert.nodeName === '#text') {
                    createTextNode(div, nodeToInsert.textContent);
                    $(parent).append(div);
                }
                else {
                    addStartCode(div, nodeToInsert);

                    //start ends

                    //value

                    div = createNode('div', cName + ' textNode');
                    addSpanNode(div, nodeToInsert.textContent);
                    $(parent).append(div);

                    //end part
                    div = createNode('div', cName);
                    addEndCode(div, nodeToInsert.nodeName);
                    $(parent).append(div);
                }


                return parent;
            }

            function appendParent(parent, nodeToInsert) {

                if (nodeToInsert.nodeName === 'BODY') return;
                var parentdiv = createNode('div', cName + ' xmlview');
                var div = createNode('div', 'startTag');

                addStartCode(div, nodeToInsert)

                parentdiv.appendChild(div);
                //start ends
                //children
                var childDiv = createNode('div', 'xmlChildren');
                parentdiv.appendChild(childDiv);
                //end part
                div = createNode('div', 'endTag');

                addEndCode(div, nodeToInsert.nodeName);

                //parentdiv = insertClickable(parentdiv);
                parentdiv.appendChild(div);

                //return insertAfter(parent, parentdiv);
                //$(parent).after(parentdiv);
                $(parent).append(parentdiv);
                return childDiv;
            }

            function addStartCode(parent, node) {

                addSpanNode(parent, '<');
                addSpanNode(parent, node.nodeName, 'tag');
                //attributes
                addAttributes(node, parent);
                addSpanNode(parent, '>');

            }

            function addEndCode(parent, name) {

                addSpanNode(parent, '</');
                addSpanNode(parent, name, 'tag');
                addSpanNode(parent, '>');
            }

            function addAttributes(node, holder) {

                if (!node.attributes) return;

                for (var i = 0, l = node.attributes.length; i < l; i++) {
                    var attr = node.attributes[i];
                    if (attr.name === 'id') {
                        _id = attr.value;
                    }
                    addSpanNode(holder, ' ' + attr.name + ' ');
                    addSpanNode(holder, ' ="');
                    addSpanNode(holder, attr.value + '"');
                }

            }

            function insertAfter(parent, child) {
                var _child = child.cloneNode();
                $(parent).after(child);
                return _child;
            }

            function insertClickable(parent) {
                var _node = createNode('span', 'clickable');
                _node.innerText = '-';
                parent.appendChild(_node);
                //$(node).prepend(_node);
                return _node;
            }

            function createTree(element, content) {
                $(element).append(content);
            }

        }
