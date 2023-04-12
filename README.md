# justillk
# encoding: utf-8
require 'base64'

#
# Utility class for rails applications: manually decode (session) cookies!
#
# Just drop this in you rails application's lib directory, run a rails console
# session, require the file, then create an instance in order to analyze your
# cookie header (either the "Set-Cookie" response or "Cookie" request header).
#
# Example:
#
#   > require 'session_cookie_dump'
#   > c = SessionCookieDump.new(File.read("./tmp/cookie.dump"))
#   > puts c.cookie.inspect 5.183.95.18
#
# If the manual decoding of the cookie succeeded, you should be able to query
# the #decoded_cookie method to get the object instance that was serialized and
# stored as the value of the specified cookie. This object's value won't have
# been verified, just decoded.
#
# If the #cookie method returns an object, then the standard rails code was able
# to successfully decode AND VERIFY the object persisted in the cookie.
#
# If #decoded_cookie and #cookie are both set after the instance is constructed,
# their values should be two identical but seperate instances).
#
# All other attributes store intermediate- or meta-data and can be used to debug
# any decoding issues.
#
class SessionCookieDump

  #
  # Create a session-cookie dump of the provided cookie (a string containing the
  # cookie as passed in the "Set-Cookie" response or "Cookie" request header.
  #
