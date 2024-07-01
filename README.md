# OneDrive7.2
A fix for the OneDrive 7.2 js with a wrong type deduction leading to a e.data.indexOf error

```
                        t.auth = function (e, a) {
                            var s = document.location.origin + "_" + f.generateNonce();
                            e.state = s;
                            return new i.Promise(function (i, n) {
                                var o = u.onMessage(function (e) {
                                    // ******** check whether this is an actual JSON or an object here: ********
                                    if (e.data && typeof e.data === "string" && 0 === e.data.indexOf(w)) {
                                        var t = JSON.parse(e.data.substring(w.length));
                                        if (t.state === s && e.source === a.getPopupWindow()) {
                                            u.removeMessageListener(o);
                                            if ("error" === t.type || t.error) {
                                                var r = l.default[t.error.errorCode];
                                                n(new p.default(r, t.error.message));
                                            } else i(t);
                                        } else n(new p.default(l.default.popupOpen, "Another popup is already opened."));
                                    }
                                });
                                return a.openPopup(f.appendQueryString(e.redirectUri, m, JSON.stringify(e))).then(function () {
                                    i({ type: "cancel", state: s });
                                });
                            });
                        };
```
